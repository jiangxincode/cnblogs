欢迎关注我的社交账号：

邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju


```
    mpirun noticed that process rank 1 with PID 3716 on node localhost.localdomain exited on signal 11 (Segmentation fault).
```

如果使用intel的编译器，当体系一大，刚进入主循环就会退出来，并提示上面的错误！一般是内存溢出了，原因在于编译时INTEL默认将缓存写在堆栈里，堆栈小时便会出现上述错误，可以尝试在编译VASP时，在FFLAGS里加上参数-heap-arrays  64，如果还不行的话，就换一下编译器，PGI应该会好点。