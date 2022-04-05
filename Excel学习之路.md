# Excel学习之路

## 书籍

* Excel 2019 Bible[EXCEL2019宝典(第10版)]: Michael Alexander,Dick Kusleika,Previously by John Walkenbach: 主力学习
* Excel 2016 Power Programming with VBA[Excel 2016高级VBA编程宝典（第8版）]: Michael Alexander,Dick Kusleika: 主力学习
* Excel 2016应用大全: 主力学习
* Excel 2007 VBA办公范例应用: 内容老旧，阅读人数少，不适合学习
* Excel 2010实用技巧集锦: 内容老旧，阅读人数少，不适合学习
* Excel VBA实战技巧精粹: 评价不错
* Excel 2010 VBA编程与实践: 已经有了《Excel 2013 VBA编程与实践》，但是后者找不到对应的电子版。前者评价还不错
* Excel VBA程序开发自学宝典(第3版): 已经有了，但是后者找不到对应的电子版。前者评价还不错

## 函数

• All functions (alphabetical): <https://support.microsoft.com/en-us/office/excel-functions-alphabetical-b3944572-255d-4efb-bb96-c6d90033e188>
• IFS function: <https://support.microsoft.com/en-us/office/ifs-function-36329a26-37b2-467c-972b-4a39bd951d45>
• SWITCH function: <https://support.microsoft.com/en-us/office/switch-function-47ab33c0-28ce-4530-8a45-d532ec4aa25e>

## 小知识点

### 改变日期格式

```shell
# 'Fri Mar 18 22:49:05 2022 +0800'->'20220318 22:49:05'
# =MID(C1, 21,4)&TEXT(MONTH(MID(C1,5,3)&"-1"), "00")&MID(C1,9,2)&" "&MID(C1,12,8)
# 如果有点时间格式不稳定，如'Fri Mar 8 22:49:05 2022 +0800'，则先分列再处理
```
