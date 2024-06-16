欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

现在各种编程语言都有自己的lint工具来做静态检查，防止一些低级错误并维持统一的风格。Markdown这样的样式标记语言也不例外，现在大家用的比较多的是markdownlint。该项目开源在github:<https://github.com/markdownlint/markdownlint>，当前很多实用markdown语言的项目都使用该工具。

markdownlint的检查规则目前有41项<https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md>，其中"MD034 - Bare URL used"是大家经常遇到的问题，如果你在Markdown文档中使用URL，但是没有在URL周围使用<>的话就会产生警告，我维护了一个类似于awesome的项目<https://github.com/jiangxincode/cnblogs>，其中报了1000多个类似的警告，如果全部手工来修改估计手都回废掉，因此写了个小程序在所有的.md文档中的所有url两遍加上了<>。

程序使用Java编写，比较简单，主要使用了正则表达式的替换，程序如下：

```java
package edu.jiangxin.tools;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Solve the problem of MD034. <p>
 * {@link https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md}
 * This program doesn't process any exception!
 * @author aloys
 *
 */
public class MD034Solver {
    public static final String regex = "\\b(https?|ftp|file)://[-A-Z0-9+&@#/%?=~_|$!:,.;]*[A-Z0-9+&@#/%=~_|$]";
    
    public static final String sourceDirStr = "D:\\temp\\cnblogs";
    
    public static final String targetDirStr = "D:\\temp\\cnblogsbak";

    public static void main(String[] args) throws IOException {
        // Source directory must be a valid directory which contains the text files to be processed.
        File sourceDir = new File(sourceDirStr);

        // Target directory must be a valid directory which will save the proecessed files.
        File targetDir = new File(targetDirStr);

        for (File file : sourceDir.listFiles()) {

            // take off the .git directory and .gitignore file
            if (file.getName().startsWith(".")) {
                continue;
            }

            BufferedReader reader = new BufferedReader(new FileReader(file));
            BufferedWriter writer = new BufferedWriter(new FileWriter(new File(targetDir, file.getName())));

            String temp = null;
            while ((temp = reader.readLine()) != null) {
                Pattern pattern = Pattern.compile(regex, Pattern.CASE_INSENSITIVE | Pattern.UNICODE_CASE);
                Matcher regexMatcher = pattern.matcher(temp);
                StringBuffer sb = new StringBuffer();
                while (regexMatcher.find()) {
                    String group = regexMatcher.group();
                    int start = regexMatcher.start();
                    if (start >= 1 && (temp.charAt(start - 1) == '<' || temp.charAt(start - 1) == '(')) {
                        regexMatcher.appendReplacement(sb, group);
                    } else {
                        regexMatcher.appendReplacement(sb, "<" + group + ">");
                    }

                }
                regexMatcher.appendTail(sb);
                writer.write(sb.toString());
                writer.newLine();
            }
            reader.close();
            writer.close();
        }
    }

}

```