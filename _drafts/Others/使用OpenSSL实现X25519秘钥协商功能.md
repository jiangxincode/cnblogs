首先大体了解下X5519曲线算法和ECC椭圆曲线算法，ECC是Elliptic curve cryptography(椭圆曲线密码学)的缩写，严格的讲X25519算法也是椭圆曲线算法的一种，但是和其他椭圆曲线算法不兼容（如secp256k1/secp354r1/secp521k1/prime256v1），所以OpenSSL最新版本虽然支持ECC算法，但是用法和其他椭圆曲线算法不同，相关情况可以参考：

* X25519（Curve25519）椭圆曲线参考资料：<https://www.jianshu.com/p/5dba044f67b1>
* OpenSSL在使用X25519时的小坑：<https://blog.csdn.net/qmickecs/article/details/73193108>
* 如何使用X25519派生共享秘钥：<https://github.com/project-everest/hacl-star/blob/master/tests/benchmark/bench_curve25519.cpp>

问题在于我们使用时需要拿到X25519公钥和私钥的unsigned char*类型数据，但是OpenSSL在生成密钥对和派生共享密钥时都是用使用EVP_PKEY类型，对于一般的椭圆曲线算法，我们可以使用i2d_PublicKey/d21_PublicKey/i2d_PrivateKey/d21_PrivateKey进行两种类型的转换：

* EVP_PKEY from char buffer in x509 (PKCS7)：<https://stackoverflow.com/questions/2918923/evp-pkey-from-char-buffer-in-x509-pkcs7>

但是结合如下链接以及查看OpenSSL源码，发现这四个方法根本不适用EVP_PKEY_X25519类型，调用时直接返回-1。

* <https://www.mail-archive.com/mailto:openssl-commits@openssl.org/msg20218.html>
* <https://github.com/openssl/openssl/pull/8168/commits/d3530f99473293a8fd5d309931e9021a7469deb2>

从以下链接中可以获取一些OpenSSL常用的转换策略，但是仍然不适用于X25519：

* How does one access the raw ECDH public key, private key and params inside OpenSSL's EVP_PKEY structure? <https://stackoverflow.com/questions/18155559/how-does-one-access-the-raw-ecdh-public-key-private-key-and-params-inside-opens>

后来发现Stack Overflow的相关提问涉及到了ecx_get_priv_key/ecx_get_pub_key两个函数，但是这两个函数都是internal的，并没有暴露给开发者，所以这条路也走不通

* How to use ecx get_priv/pub_key methods from openssl? <https://stackoverflow.com/questions/59468839/how-to-use-ecx-get-priv-pub-key-methods-from-openssl>

最后翻了下OpenSSL的Github issues，发现不少人遇到了这个问题：

* It's not possible to export the raw public key for X25519/Ed255919/X448/Ed448：<https://github.com/openssl/openssl/issues/6259>
* Add getters for raw private/public keys：<https://github.com/openssl/openssl/pull/6394>

从大家的讨论中发现OpenSSL的commiter在1.1.1版本提供了EVP_PKEY_get_raw_private_key和EVP_PKEY_get_raw_public_key，经验证可以使用：

* <https://github.com/openssl/openssl/commit/0d124b0a51d3ad8c8807cab280ea18fc68489155>