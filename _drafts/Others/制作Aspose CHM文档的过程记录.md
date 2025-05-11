
最近公司需要使用Aspose组件开发相关内容，但是网上找不到理想的参考文档，官网访问速度也慢的可以。所以打算自己做份CHM文档，做的过程中遇到很多困难，这里记录一下。
第一步是在Aspose官网上把javadoc文档爬取出来，我使用的工具是TeleportPro。爬取的网址是

* http://www.aspose.com/api/java/pdf
* http://www.aspose.com/api/java/cells

经过尝试爬取深度设为7最好。爬出来发现内容很多，有一个多G，而且有很多杂乱的内容，我们知道一般javadoc文档只是html和css的组合，不需要js和各种图片，所以仅保留了合适的目录下的html文档和api-reference-ui.css文件，其余文件全部删除。

但是这是发现由于删除了一些文件，导致html文件中对api-reference-ui.css引用失效，于是用notepad++对引用路径进行批量替换（../../../apireference.dynabic.com/doc/resources/css/api-reference-ui.css -> api-reference-ui.css），这时保证CSS文件能够正常引用，但是用这些文件生成的chm文档仍然很大，并且有一些无用的按钮无法点击，然后我们需要把它们干掉。于是我写了一个java程序，进行操作，需要最新的程序或者有不理解的可以联系我：

```java
package edu.jiangxin.tools;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.util.ArrayList;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import edu.jiangxin.common.FileFilterWrapper;

public class RemoveHtmlElement {

	static final String charsetName = "UTF-8";
	static final String[] divClassNames = { "Header", "aspNetHidden", "Search", "clearAll", "Header" };
	static final String[] divIds = { "Header", "leftmenu" };

	public static void main(String[] args) throws IOException {
		ArrayList<File> files = new FileFilterWrapper().list("C:/asposebak", "htm");
		for (File file : files) {
			Document doc = Jsoup.parse(file, charsetName);
			for (int i = 0; i < divClassNames.length; i++) {
				Elements eles = doc.getElementsByClass(divClassNames[i]); // eles不可能为null

				eles.remove();
			}
			for (int i = 0; i < divIds.length; i++) {
				Element ele = doc.getElementById(divIds[i]);
				if (ele != null) {
					ele.remove();
				}

			}

			Elements eles = doc.getElementsByTag("script");
			for (int i = 0; i < eles.size(); i++) {
				Element ele = eles.get(i);
				if (ele.attr("language").equals("javascript") && ele.attr("type").equals("text/javascript")) {
					ele.remove();
				}
			}

			FileOutputStream fos = new FileOutputStream(file, false);
			OutputStreamWriter osw = new OutputStreamWriter(fos, charsetName);
			osw.write(doc.html());
			osw.close();
			System.out.println(file.getAbsolutePath());
		}
	}

}


```

通过程序删除之后基本解很清爽了，当然还需要使用notepad++进行一些简单的文本批量替换。
最后的工作就是使用easychm生成chm文档了，我用的是试用版，感觉只不过多了广告，生成的chm文档并不影响使用。