# Pyside6

当我们选择使用Python来编写大型程序的时候，我们会遇到程序得是GUI的形式，
毕竟如果是CUI的话，我们一般来说称之为工具。

于是乎我们开始纠结，Python的哪个GUI框架对于我们来说比较好，
我对此做了一定程度的调研。


## PyQt 和 Pyside

根据一些资料,PyQt由Riverbank Computing Ltd的Phil Thompson开发。
并且已经存在了很长一段时间-支持Qt的版本可以追溯到2.x。
2009年，当时拥有Qt工具包的诺基亚希望以更宽松的LGPL许可证提供Qt的Python绑定。

1. [PyQt6 vs PySide6](https://www.pythonguis.com/faq/pyqt6-vs-pyside6/)
2. [PyQt、PySide、PySide2这三者到底有什么区别？](https://blog.csdn.net/luoyayun361/article/details/99281515)

这里需要说明，根据[PyQT官网](https://www.riverbankcomputing.com/software/pyqt/intro)的说明，License许可证实际上是有遵循GNU GPL v3和Riverbank Commercial License的
这意味着，如果你的软件使用了PyQt，如果你没有购买商业许可的话，你就必须要开源你的软件，当然很多公司并没有遵守这一规定。

### 现状

参考知乎上的一个回答:[如何评价Qt官方推出的Qt for Python(PySide)？](https://www.zhihu.com/question/306793447)
前因后果应该就是一开始PyQt是另外一家公司维护和开发的，后来Qt的开发商想自己自主开发，这也是Pyside(Qt for Python)项目的来源。
经过了风雨飘摇的几年后，Pyside已经发展的非常成熟了，推出了Pyside2（对标Qt 5）以及现在的Pyside6（对标Qt 6）


### 教程

推荐学习教程如下：

我推荐

1. [https://www.pythonguis.com/pyside6/](https://www.pythonguis.com/pyside6/)