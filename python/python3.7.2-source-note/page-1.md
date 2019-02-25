# 第1章 Python对象初探


## 1.1 Python内的对象



### 1.1.1 对象机制的基石--PyObject


`PyObject`结构体定义：

```
typedef struct _object {
    _PyObject_HEAD_EXTRA
    Py_ssize_t ob_refcnt;
    struct _typeobject *ob_type;
} PyObject;

```

首先看第一个东西：`_PyObject_HEAD_EXTRA`。

定义：

```
#ifdef Py_TRACE_REFS
/* Define pointers to support a doubly-linked list of all live heap objects. */
#define _PyObject_HEAD_EXTRA            \
    struct _object *_ob_next;           \
    struct _object *_ob_prev;

#define _PyObject_EXTRA_INIT 0, 0,

#else
#define _PyObject_HEAD_EXTRA
#define _PyObject_EXTRA_INIT
#endif
```

在正常运行Python程序的时候，是没有定义`Py_TRACE_REFS`的。

*定义`Py_TRACE_REFS`的话，会启用**reference tracing**，并且在`PyObject`中添加两个指针，将各个对象组成双向链表。同时会 Total allocations are tracked as well。 退出的时候，将会打印所有`existing references`(交互模式下，在解析器运行每个语句后触发）*

*注：使用英语是由于不知道该怎么翻译*

由于上面的原因，`PyObject`可以简化成

```
typedef struct _object {
    Py_ssize_t ob_refcnt;
    struct _typeobject *ob_type;
} PyObject;
```

其中，`ob_refcnt`与Python内存管理机制有关。Python使用基于**引用计数**的垃圾回收机制。

举个例子，有个对象A：
- 在实例化A的时候，A的引用计数加1；
- 在删除A的实例的时候，A的引用计数减1；
- 当A的引用计数等于0的时候，A就可以从堆中移除，目的是释放A占用的内存。

`ob_refcnt`就是**引用计数**啦。


可以看到，`ob_type`是指向*_typeobject*结构体的指针。

> 实际上这个结构体对应着Python内部的一种特殊对象，它是用来指定一个对象类型的类型对象。 -- 《Python源码剖析：深度探索动态语言核心技术》


对比《Python源码剖析：深度探索动态语言核心技术》书中内容和Python-3.7.2源码，可以看出Python的对象机制的核心在3.7.2版本仍然保持着和2.5版本一样简单。


没有任何东西声明为`PyObject`，实际情况是每个指向Python对象的指针可以转换成`PyObject *`（手动强制转换，参考代码:`cpython/Python/traceback.c`）。



### 1.1.2 定长对象和不定长对象

TODO

## 1.2 类型对象

TODO


### 1.2.1 对象的创建

TODO


### 1.2.2 对象的行为

TODO

### 1.2.3 类型的类型

TODO

## 1.3 Python对象的多态性

TODO

## 1.4 引用计数

宏`Py_inCREF(op)`和`Py_DECREF(op)`用于添加或者减少引用计数。在引用计数等于0的时候，`Py_DECREF`会调用对象对象的析构函数(对应python中的`__del__`、源码中的`tp_dealloc`)。


需要注意的是，调用析构函数并不意味着一定会释放内存空间。 之前有看到过说，Python如果某个对象驻留时间比较长，在调用析构函数的时候，相对来说释放内存空间会晚一点。具体待验证(TODO)


## 1.5 Python对象的分类



TODO
