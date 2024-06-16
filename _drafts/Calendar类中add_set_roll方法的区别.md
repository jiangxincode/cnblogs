欢迎和大家交流技术相关问题：

* 邮箱: jiangxinnju@163.com
* 博客园地址: http://www.cnblogs.com/jiangxinnju
* GitHub地址: https://github.com/jiangxincode
* 知乎地址: https://www.zhihu.com/people/jiangxinnju

Calendar类中有三个方法更改日期的某个字段：set()、add() 和 roll()。
 
set(f, value) 将日历字段 f 更改为 value。此外，它设置了一个内部成员变量，以指示日历字段 f 已经被更改。尽管日历字段 f 是立即更改的，但是直到下次调用 get()、getTime()、getTimeInMillis()、add() 或 roll()时才会重新计算日历的时间值（以毫秒为单位）。因此，多次调用 set() 不会触发多次不必要的计算。使用 set()更改日历字段的结果是，其他日历字段也可能发生更改，这取决于日历字段、日历字段值和日历系统。此外，在重新计算日历字段之后，get(f) 没必要通过调用 set 方法返回 value 集合。具体细节是通过具体的日历类确定的。

示例：假定 GregorianCalendar 最初被设置为 1999 年 8 月 31 日。调用 set(Calendar.MONTH, Calendar.SEPTEMBER) 将该日期设置为 1999 年 9 月 31 日。如果随后调用 getTime()，那么这是解析 1999 年 10 月 1 日的一个暂时内部表示。但是，在调用 getTime() 之前调用 set(Calendar.DAY_OF_MONTH, 30) 会将该日期设置为 1999 年 9 月 30 日，因为在调用 set() 之后没有发生重新计算。

add(f, delta) 将 delta 添加到 f 字段中。这等同于调用 set(f, get(f) + delta)，但要带以下两个调整：

* Add 规则 1。调用后 f 字段的值减去调用前 f 字段的值等于 delta，以字段 f 中发生的任何溢出为模。溢出发生在字段值超出其范围时，结果，下一个更大的字段会递增或递减，并将字段值调整回其范围内。

* Add 规则 2。如果期望某一个更小的字段是不变的，但让它等于以前的值是不可能的，因为在字段 f发生更改之后，或者在出现其他约束之后，比如时区偏移量发生更改，它的最大值和最小值也在发生更改，然后它的值被调整为尽量接近于所期望的值。更小的字段表示一个更小的时间单元。HOUR 是一个比 DAY_OF_MONTH 小的字段。对于不期望是不变字段的更小字段，无需进行任何调整。日历系统会确定期望不变的那些字段。

此外，与 set() 不同，add() 强迫日历系统立即重新计算日历的毫秒数和所有字段。

示例：假定 GregorianCalendar 最初被设置为 1999 年 8 月 31 日。调用 add(Calendar.MONTH, 13) 将日历设置为 2000 年 9 月 30 日。Add 规则 1 将 MONTH 字段设置为 September，因为向 August 添加 13 个月得出的就是下一年的 September。因为在 GregorianCalendar 中，DAY_OF_MONTH 不可能是 9 月 31 日，所以 add 规则 2 将DAY_OF_MONTH 设置为 30，即最可能的值。尽管它是一个更小的字段，但不能根据规则 2 调整 DAY_OF_WEEK，因为在 GregorianCalendar 中的月份发生变化时，该值也需要发生变化。

roll(f, delta) 将 delta 添加到 f 字段中，但不更改更大的字段。这等同于调用 add(f, delta)，但要带以下调整：

* Roll 规则。在完成调用后，更大的字段无变化。更大的字段表示一个更大的时间单元。DAY_OF_MONTH是一个比 HOUR 大的字段。

示例：请参阅 GregorianCalendar.roll(int, int)。

使用模型。为了帮助理解 add() 和 roll() 的行为，假定有一个用户界面组件，它带有用于月、日、年和底层GregorianCalendar 的递增或递减按钮。如果从界面上读取的日期为 1999 年 1 月 31 日，并且用户按下月份的递增按钮，那么应该得到什么？如果底层实现使用 set()，那么可以将该日期读为 1999 年 3 月 3 日。更好的结果是 1999 年 2 月 28 日。此外，如果用户再次按下月份的递增按钮，那么该日期应该读为 1999 年 3 月 31 日，而不是 1999 年 3 月 28 日。通过保存原始日期并使用 add() 或 roll()，根据是否会影响更大的字段，用户界面可以像大多数用户所期望的那样运行。

假设:f= 2001-1-30 
f.add(Calendar.MONTH, 13) = 2002.2.28 
f.set(Calendar.MONTH,1) =  2002.3.2 
f.roll(Calendar.MONTH, 13) = 2001.2.28
 
Add:修改后如果符合实际，会调整，但不会改变调整的值，如例子中的MONTH。 
Set: 会改变如把2月改为3月。 
roll：于Add类似，不同在于不会改变更大的日期单位，如还是2001 不会为2002。 

下面为代码演示：

```java 
    Calendar c=Calendar.getInstance();
    //c.setTimeInMillis(System.currentTimeMillis());

    c.set(2001,0,30);
    c.add(Calendar.MONTH, 13); 
    System.out.println(c.getTime().toString()); 
    c.set(2001,0,30);
    c.set(Calendar.MONTH,1); 
    System.out.println(c.getTime().toString()); 
    c.set(2001,0,30);
    c.roll(Calendar.MONTH, 13); 
    System.out.println(c.getTime().toString()); 
```

结果：

```
    Thu Feb 28 10:22:37 CST 2002
    Fri Mar 02 10:22:37 CST 2001
    Wed Feb 28 10:22:37 CST 2001
```

注意，Calendar.MONTH是从0开始的，也就是说一月用0表示