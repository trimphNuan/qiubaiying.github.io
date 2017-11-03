---
layout: post
date: 2017-11-03
subtitle:   python_super分析 #副标题
author:     trimphNuan                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - python
---


### super 继承解析

  首先没有super我们如何调用父类属性，或者方法：


    ### super 构造方法 有两个默认参数
    def __init__(self, type1=None, type2=None):  # known special case of super.__init__
        #type1 表示 当前类
        #type2 表示 当前类实例
        pass

    ### 不用super
    class A(object):

     def __init__(self):
         print("enter A")


    class B(A):
     def __init__(self):
         print('enter B')
         A.__init__(self)
    B()

    print("=================")


    #使用super
    class A(object):

     def __init__(self):
         print("enter A")


    class B(A):
     def __init__(self):
         print('enter B')
         super().__init__()  ## super     好处是 当继承关系发生改变时我们不用修改代码就可以调用父类方法

    B()


    ### super 构造方法 有两个默认参数
    def __init__(self, type1=None, type2=None):  # known special case of super.__init__
      #  type1 表示 当前类
      #  type2 表示 当前类实例
      pass


     输出：：
      enter B
      enter A
      =================
      enter B
      enter A  


    ### 下面我们看下面的一段代码
    class DescriptorOwner(type):
        def __new__(cls, name, bases, attrs):
            # find all descriptors, auto-set their labels
            for n, v in attrs.items():
                 print("n")
            return super(DeprecationWarning,cls).__new__(cls, name, bases, attrs)
            # cls 类似 类方法的第一个参数 self
            #  DeprecationWarning  表示当前类  通过它找到它的父类 然后通过 self实例 转化为父类的实例  这样就可以调用父类的__new__() 方法了
