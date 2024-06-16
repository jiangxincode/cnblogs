在网络安全技术领域中各种加密解密算法的软件实现上始终有一个共同的问题就是如何在普通的PC机上实现大数的运算。我们日常生活中所应用的PC机内部字长多是32位或64位，但是在各种加密解密的算法中为了达到一定的安全强度，都是要求在128位、512位或者是1024位这样的字长下进行加减乘除模逆等各种数学运算，我们称为大数运算。在这样的前提下，如何在PC机上快速高效的实现大数运算就很自然的成为了在PC机上实现加密解密算法最为基础和重要的问题。像Python、Lisp等语言都内建了大数计算机制，但是像C/C++语言既没有内建大数运算机制也没有对应的标准库实现。

为了解决C/C++大数运算的问题，许多优秀的大数运算库随之出现。下面对几种优秀的大数库进行简单的介绍：

GMP：GMP大数库是GNU项目的一部分，诞生于1991年。作为一个任意精度的大整数运算库，它包括了任意精度的整数、浮点数的各种基本运算操作。它是一个C语言的库，但是官方提供了C++的包装类，主要的应用方向是密码学、网络安全、代数系统、计算科学等。GMP库的运行速度非常快，它的官方网站上称自己为地球上最快的大数库，但是GMP库所提供的只是数学运算功能，并没有密码学相关的高级功能。（注：GMP安装如果出现了问题，可能是安装包所在目录太深了，试着换个目录重新安装下）

Miracl：Miracl库是Shamus Software Ltd开发的一个大数库，它的使用许可针对教育科学研究或者非商业目的的应用是免费的。它是一个C语言的库，同时提供了几个较为简单的c++包装类。在功能上它不但提供了高精度的大整数和分数的各种数学运算操作而且提供了很多密码学算法中的功能模块，如SHA、AES、DSA等中的一些底层操作。最为特别的是它还提供了很多椭圆曲线密码体制中的底层功能模块。由于Miracl库的内部实现采用了很多的汇编代码，故运行速度也非常快。

Crypto++：Crypto++库是一个开源项目。由于它是一个纯C++实现的库，所以应用非常的方便，库的结构清晰，文档也很健全。Crypto++库提供了很多密码学算法的实现。

OpenSSL：OpenSSL是一个开放源代码的实现了SSL及相关加密技术的软件包，由加拿大的Eric Yang等发起编写的。它可以实现消息摘要、文件的加密和解密、数字证书、数字签名和随机数字等。它的主要用途并不是大数库，而是SSL协议的实现和应用，但是其中也有一些关于大整数的功能，此外它也是基于C语言。

下面是一些常用的大数运算库的地址（有些虽然不是专门的大数运算库，但是带有相关的库）

Crypto++：<http://www.eskimo.com/~weidai/cryptlib.html>

MIRACL：<https://github.com/CertiVox/MIRACL>

GNU MP：<http://www.swox.com/gmp/>

Piologie： <http://www.hipilib.de/pidownload.htm>

cryptlib：<http://www.cs.auckland.ac.nz/~pgut001/cryptlib/>

RSAEuro：<http://www.rsaeuro.com/products/RSAEuro/>

OpenSSL：<http://www.openssl.org/>

RSARef：<http://download.gale.org/rsaref20.tar.Z>

GInt：<http://triade.studentenweb.org/GInt/gint.html>（Delphi）