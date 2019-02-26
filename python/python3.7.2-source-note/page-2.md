# 第二章 Python中的整数对象



## 2.1 初识PyLongObject对象


在python2上，整数类型有`int`和`long`，但是在Python3中只有`int`类型。实际上Python3的`int`类型是Python2中的`Long`类型，而原来Python2的`int`类型在Python3中已经被移除。因此Python3的`int`类型对应的C-API名字从`PyInt_*`替换成`PyLong_*`。


