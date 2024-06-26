﻿﻿


最近写了一个Cache的模拟器，由于平时空余时间比较分散，前前后后用了一周多的时间，基本实现的Cache的模拟功能（通过读取trace文件得到相应的命中率），能够实现直接映射、全相联、组相联三种映射方式，其中全相联和组相联能够实现随机、LRU两种替换策略。目前三种映射方式均采用回写法，但已经定义了其它写策略的接口，可以很容易扩充。程序具有比较强的鲁棒性，能够接受一定范围的错误输入，并能够比较智能的提示用户输入。

我尽量缩减了不必要的代码，控制在1000行以内。但日后加上部分功能后，可能会远超这个数目，希望大家帮我优化一下代码，以提高程序的空间效率。时间效率也不是很高，至少现在来说，读取30万行的内存地址数据，如果采取全相联的话，需要耗费的时间还是很长的。我会尽量优化。

程序使用C/C++混合编程，但不是采用面向对象的方法，虽然在编写过程中想改成以类的方式实现，但是整体框架已经完成的差不多了，所以就没有改。程序中使用了一些C++11标准中的类，比如bitset<T>，所以必须在支持C++11的编译器上进行编译，但现在主流的编译器比如gcc和VS均已支持，所以不用太担心。

我已经上传了代码和可执行程序的最新版本，下载地址是：

http://download.csdn.net/detail/jiangxinnju/7404137

程序能够在Windows平台下直接运行，如果你想在Linux平台运行，请重新编译，并调整base.h中相应的编译选项，其它文件不用修改，因为我已经使用了条件编译适应不同的编译环境。如果你只是想查看最后的数据结果，不关心每条数据的具体命中情况请不要在编译的时候注释掉

#define NDEBUG // For NDEBUG pattern

否则，程序需要很长的运行时间。另外如果你希望看到本程序的历史版本，或者希望在我的程序中添加新的功能，可以直接fork我的github，地址为：

https://github.com/jiangxincode/CacheSim

关于本程序的版权声明，可以参考README.txt文件，在遵守相关条目的基础上，你可以任意拷贝、修改我的程序。

如果你对于程序中的内容有所疑问，比如无法在你的机器上正常编译或运行，可以直接联系我，我的Email地址为：

jiangxinnju@163.com

欢迎各位朋友提出修改意见。

﻿﻿