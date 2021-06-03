# 段错误解决方案


```shell
$ ulimit -c 100000
$ ./test                       // 这一步会创建一个类似core.21203的文件
$ gdb ./test core.21203
(gdb) where                    // 通常到这里会打印出具体哪行代码报错
```


*注意*:
- 如果用cmake编译，需要在 CMakeLists.txt 加一些配置
- 有时候会缺系统依赖，注意看gdb上的打印，缺啥装啥
