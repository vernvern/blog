# 段错误解决方案


```shell
$ ulimit -c 100000             // 原来的值一般是0， 如果 填大于0（例如这里填了）  100000，再执行程序，会产生一个 core.pid 文件。
$ ./test                       // 原来执行 ./test 是正常跑，因为上面的命令，导致这一步结束后(段错误)会在当前目录创建一个类似core.21203的文件
$ gdb ./test core.21203
(gdb) where                    // 通常到这里会打印出具体哪行代码报错
```


*注意*:
- 如果用cmake编译，需要在 CMakeLists.txt 加一些配置
- 有时候会缺系统依赖，注意看gdb上的打印，缺啥装啥
