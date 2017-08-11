.. title: Julia Notes
.. slug: julia-notes
.. date: 2016-05-24 12:22:41 UTC+08:00
.. tags: julia
.. category: programming
.. link:
.. description:
.. type: text
.. author: YONG

安装
======

1. 下载并安装64-bit Julia (command line version), 可选择自定义的安装路径.
2. 新建环境变量 ``JULIA_HOME``, 并指向 ``Julia`` 的 ``\bin`` 目录.
3. 在 ``PATH`` 环境变量下添加 ``%JULIA_HOME%``.

.. TEASER_END

REPL 基础
==========

系统命令

===================     ===========================================
ans                     上一次计算结果
?                       help mode, 等同于 help(xxx)
apropos("quit")         搜索和quit相关的命令
methods(filter)         查看filter函数详细信息
;                       shell mode
whos()                  查看全局变量信息
@which sin(3)           查看sin(3)命令中调用了哪些method
edit("filename")        编辑文档
less("filename")        显示文档
clipboard("stuff")      将"stuff"拷贝到系统剪贴板
clipboard()             将剪贴板当前内容拷至当前REPL
dump()                  显示一个Julia object相关信息
names()                 显示某个module的所有exported names
workspace()             替换top-level module(Main), 并清除workspace
===================     ===========================================

按键

===================     ===========================================
Up/Down                 显示之前输入的命令
Ctrl-R/Ctrl-S           搜索之前输出的内容
===================     ===========================================

语法

===========================         ===========================================
``+(2,3,4)``                        等同于 ``2+3+4``
``pi``, ``golden``, ``e``           系统预定义常量
``666//999``                        ``//`` 用于rational number
``y\x``                             ``\`` 为reverse division, ``x/y=y\x``
``+=``, ``-=``, ...                 这些符号也是允许的
``[2,4].*[10,20]``                  element-wise operation
``a,b=5,3``                         assign multiple variables, 返回类型: tuple
``\sqrt<TAB>``                      转换成LaTeX字符
===========================         ===========================================

数制

================            ====================================================
bits(20.0)                  shows the literal binary representation of a number
hex(), oct()                to hex or oct
base(16, 266)               to a string in given base
================            ====================================================

Arrays and Tuples
==================

Julia arrays are "column-major" (列主序). This means that you read down the columns:

.. code:: shell

    1 3
    2 4

* Column-major order: Fortran, R, Matlab, GNU Octave, BLAS, LAPACK, OpenGL/OpenGL ES, Julia
* ROW-major order: C/C++, Mathematica, Pascal, Python, C#/CLI/.Net, Direct3D

Simple arrays
~~~~~~~~~~~~~~~

========================    =========================================================
s=[1, 2.0, 3]               创建一个array, 类型为Float64
trifuns=[sin, cos, tan]     一个函数array
array=Array(Int64,5,2)      创建一个array, 并指定类型与大小, 等同于Array{Int64}(5,2)
[1, "2", sin, 3.0]          同一个array可以包含不同类型
typeof(ans)                 查看数据类型
Int64[1,2,3,4,5]            创建一个某种类型的array
Int64[]                     创建一个空的Int64型array, 其它类型还包括String, Float64等
========================    =========================================================

Row vectors
~~~~~~~~~~~~~~~~~~~~~~~

========================    =========================================================
[1 2 3 4]                   1x4 Int64 array (row vector)
[1 2 3; 5 6 7]              2x3 Int64 matrix
========================    =========================================================

在julia中, column vector是一维矩阵, 而row vector是二维矩阵, 大概julia也是偏好列向量的计算系统. 比如:

.. code:: shell

    julia> [1,2,3]
    3-element Array{Int64,1}:
     1
     2
     3

    julia> [1 2 3]
    1x3 Array{Int64,2}:
     1  2  3

可以看出, 列向量是Array{Int64,1}类型而行向量是Array{Int64,2}

Range objects
~~~~~~~~~~~~~~

``1:10`` 等同于 ``range(1,10)``, 用途:

1. 生成列向量. 比如 ``[1:10]``, 或 ``collect(1:10)``
2. loop表达式: ``for n in 1:10 print(n) end``

``[0:10:100]`` 从0到100(包括100), 步长10. 亦可用于浮点类型.

``linspace(1,100,12)`` 从1到100, 12步, 即会产生12个数. 另一个类似函数是 ``logspace()``, 即它的 logarithmic 版本.

Matrix
~~~~~~~~~

创建
######

创建一个2x3矩阵, 可使用:

1. ``[1 2 3; 4 5 6]`` (按行创建),
2. 按列创建: ``[[1, 2, 3] [4,5,6]]``
3.  ``Array(Int64, 3,2)`` 创建一个二维矩阵
4. ``reshape([1,2,3,4,5,6], 2, 3)``, 即将一个简单数组或矩阵变为想要形状.

``b=similar(a)``        拷贝矩阵a给b(只拷形式作初始化用, 不拷数据)

初始化
######

1. ``collect(0:10:100)`` 创建列向量并赋值
2. 使用 zeros, ones, trues, flases, fill, fill!, rand, randn, eye, diagm 等函数.
3. 创建简单的向量后使用 reshape 转换成多维矩阵.
4. Comprehensions, 如 ``[r*c for r in 1:5, c in 1:5]``

元素indexing
#############

1. 元素索引格式为 a[5], a[2,3] 这样的形式, 或者 getindex(a, 1, 3)
2. 行索引: a[1, :] (单行), 或者 a[1:2, :] (多行)
3. 列索引: a[:,2] (单列), a[:, 1:2] (多列), a[:] 会将整个矩阵返回成一个列向量.
4. 对于二维数列(矩阵)a, indexing的时候可以有第三个分量, 试了以后貌似只能是1, 其它值都会出错. 即 a[:,2:6,1] 相当于 a[:,2:6]. 以后尽量不要用这种方式.

Tips
======

====================================================         =====================================================================================
操作                                                         说明
----------------------------------------------------         -------------------------------------------------------------------------------------
convert(Float64, i)                                          将 i 转换为Float64类型.
function parse(type, num, base=10)                           default arguments
include("filename.jl")                                       包含另一个文件
repeat([4,2], outer=[3,1])                                   得到一个6x1的2D array, 即[4,2,4,2,4,2]
readdlm("matrixdata.txt")                                    读取一个数据文件并保存为矩阵, 一般文件名都用ASCIIString类型
====================================================         =====================================================================================

Other Tips
==============

* Julia在windows下升级到最新版本只能通过下载新的exe文件安装, 覆盖安装之后再用 ``Pkg.update()`` 更新包. 另外 cmder 替换windows本身的cmd已经足够好用, 试了下并不喜欢Julia官网推荐的基于Atom的集成环境Juno IDE.
* ``for i in 1:k`` 如果 ``k`` 小于1, 循环将不会被执行.
* ``atan2(y,x)`` 结果会落在 (-pi, pi] 内, 而且Julia定义了 ``atan2(0,0)`` 等于 ``0``. 注意范围内不包括 ``-pi``, 可以验证 ``atan2(0,-1)`` 结果为 ``pi``.
* ``2pi`` 表示 ``6.283185307179586``, 类似地, 一些常量和数字可以缩写在一起.
* 可以使用 ``length()`` 获取一维array的大小, 对于二维数组, 会得到总元素个数. 想要得到多维数组的dimension信息, 需要使用 ``size()``
* ``isfile(path)`` 检测文件是否存在. ``rm(path)`` 可用于删除文件
* ``@show()`` 可以接受多个参数, 用于debug时打印出中间变量到console, 非常方便.
* ``@time`` macro加在执行命令的前面用于测试运行时间. 第一次调用时运行时间会稍长, 之后的调用会比较短. 因此以之后的为准.
* ``0^0`` 在 Julia 中被定义为1, 在Mathematica中会报错(只能说MMA比较2, 经常涉及到Bernstein的定义都要用个Switch来考虑一下特殊情况).
