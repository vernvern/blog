# 第0章 Python源码剖析--编译python


## 0.1 Python总体架构


*注: 本节内容整理自《Python源码剖析》一书，书中使用Python-2.5版本。由于笔者水平不够，对Python-3.7.2源码没有足够的理解，尚未验证3.7.2版本下Python是否仍此架构。* -- 2019/2/22 Vern. (TODO)


```
   File Groups                      Python core                        Runtime Environment


                                +---------------------+
                                |    INTERPRETER      |
                                +---------------------+
                                |                     |
                                |    +---------+      |
+--------------+                |    | Scanner |      |
| Core Modules |                |    +----+----+      |
+--------------+                |         |           |
                                |     +---v----+      |             +------------------------+
+--------------+                |     | Parser |      |             | Object/Type Structures |
|  Labrary     |       +-->     |     +---+----+      |             +------------------------+
+--------------+                |         |           |
                                |    +----v-----+     |                 +------------------+
+--------------+                |    | Compiler |     |                 | Memory Allocator |
| User+defined |                |    +----+-----+     |                 +------------------+
| Modules      |                |         |           |
+--------------+                |  +------v--------+  |             +-------------------------+
                                |  | Code Evauator |  |             | Current State of Python |
                                |  +---------------+  |             +-------------------------+
                                |                     |
                                |                     |
                                +---------------------+

                          
                            
                                    Python 总体架构（参考自《Python源码剖析》图0-1）

```

Files Groups:
- Core Modules: 内置模块
- Labrary: 系统库
- User-defined Modules: 用户编写的模块

Python core: Python的核心--解析器(interpreter)
- Scanner: 词法分析。
- Parser： 语法分析。 在Scanner(词法分析)的基础上进行语法分析，建立抽象语法树(AST)。
- Compiler: 根据建立的AST生成指令集合--Python字节码。
- Code Evauator: 执行字节码。

Runtime Environment：运行环境
- Object/Type Structures: 对象/类型系统
- Memory Allocator： 内存分配器
- Current State of Python： 运行时状态信息




## 0.2 Python源代码组织


```
.Python-3.7.2
├── Doc
├── Grammar
├── Include    
├── Lib          
├── m4
├── Mac
├── Misc
├── Modules
├── Objects
├── Parser
├── PC
├── PCbuild
├── Programs
├── Python
└── Tools

```

- Include： 包含`*.h`头文件。
- Lib: Python系统库代码存放的地方。包含`*.py`文件，可以看到像 `abc.py`、`io.py`等系统库名字的文件。
- Modules: 用C语言实现的模块存放的地方。大量`*.c`和一些`*.h`文件。
- Parser:  `TODO`
- Objects: 有很多类似`dictobject.c`、`listobject.c`的文件，应该是Python内置的对象实现代码存放的地方。
- Python: `TODO`



## 0.3 Windows环境下编译Python ~~(没有windows电脑，跳过)~~

##  0.4 Unix/Linux 环境下编译Python


官方提供 `tar.xz` 和 `tgz`两种压缩过的源码包。

解压后可以使用Linux下经典的"三剑客"完成源码编译:
- `./configure --prefix=<安装路径>`
- `make`
- `make install`


如果想要使用开发者模式的话可以使用: `./configure --with-pydebug && make -j`。


参考文献:
- [Python Developer’s Guide](https://devguide.python.org/)




## 0.5 修改Python源代码

##  0.6 通往Python之路

## 0.7 一些注意事项