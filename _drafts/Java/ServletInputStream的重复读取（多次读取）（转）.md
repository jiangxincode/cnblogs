欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

在使用Servlet进行Web开发的时候，有时候为了增加必要的业务处理而又不想修改现有的程序，往往采用Filter。这样在各个Filter中可能都要读取ServletInputStream流的内容，而ServletInputStream却只能读一次，这时候必须备份HttpServleRequest。

```java

class BufferedServletInputStream extends ServletInputStream {
	private ByteArrayInputStream inputStream;
	public BufferedServletInputStream(byte[] buffer) {
		this.inputStream = new ByteArrayInputStream( buffer );
	}
	@Override
	public int available() throws IOException {
		return inputStream.available();
	}
	@Override
	public int read() throws IOException {
		return inputStream.read();
	}
	@Override
	public int read(byte[] b, int off, int len) throws IOException {
		return inputStream.read( b, off, len );
	}
}

class BufferedServletRequestWrapper extends HttpServletRequestWrapper {
	private byte[] buffer;
	public BufferedServletRequestWrapper(HttpServletRequest request) throws IOException {
		super( request );
		InputStream is = request.getInputStream();
		ByteArrayOutputStream baos = new ByteArrayOutputStream();
		byte buff[] = new byte[ 1024 ];
		int read;
		while( ( read = is.read( buff ) ) > 0 ) {
			baos.write( buff, 0, read );
		}
		this.buffer = baos.toByteArray();
	}
	@Override
	public ServletInputStream getInputStream() throws IOException {
		return new BufferedServletInputStream( this.buffer );
	}
}

```
 
在Filter的doFilter（）或者Servlet的doPost（）中，

```java

//备份HttpServletRequest
HttpServletRequest httpRequest = (HttpServletRequest)request;
httpRequest = new BufferedServletRequestWrapper( httpRequest );
//使用流
InputStream is = request.getInputStream();
//其他业务逻辑
//将request 传到下一个Filter
chain.doFilter(request, response);

```