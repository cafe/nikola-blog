.. title: Julia for Matrix Methods
.. slug: julia-for-matrix-methods
.. date: 2017-03-01 13:59:43 UTC+08:00
.. tags: julia, tutorial, mathjax
.. category: programming
.. link:
.. description:
.. type: text

.. sectnum::

.. contents::

.. TEASER_END

.. class:: alert alert-info pull-right

.. admonition:: References:

   - `Introduction to Matrix Methods <http://stanford.edu/class/ee103/julia.html>`_
   - `Performance Tips <http://docs.julialang.org/en/stable/manual/performance-tips/>`_



Introduction
==============

Basic arithmetric & mathematical functions
---------------------------------------------

- ``+``, ``-``, ``*``, ``/``, ``^`` (exponentiate), ...
- ``true``, ``false``, ``+=``, ``!=``, ``<``, ``>``, ``<=``, ``>==``, ``!(value == 4)``, ...
- ``im`` (imaginary unit), ``pi``, ``e``, ``golden``, ...
- ``exp``, ``sqrt``, ``sin``, ``rand()``, ...
- ``typeof(x)``, ``println(23)``, ``quit()``, ``methods(sin)``, ...
- assign multiple variables (return type: Tuple): ``a,b=5,3``

  Swap two variables: ``a,b=b,a``

- convert float to int: ``Int64(3.0)`` 相当于 ``convert(Int64, 3.0``), ``ceil(Int64, 2.5)``, ``round(Int64, 2.5)``, ``floor(Int64, 2.5)``

更高精度
^^^^^^^^^^^^

对于 Float64 类型，其机器精度 machine epsilon 为 ``eps(Float64) = 2.220446049250313e-16``, 其精度 precision 是 ``precision(Float64) = 53``.
需要更高精度运算的话，可使用 Julia 自带的 BigFloat 类型或使用第三方 package, 如 "DecFP.jl", "ArbFloats.jl", "DoubleDouble.jl", "DEQuadrature.jl".

Tuples
---------

Tuples act like "immutable" arrays.

- unpack a tuple:

  .. code:: jlcon

      julia> word1, word2 = ("foo", "bar")
      ("foo","bar")

      julia> word1
      "foo"

      julia> word2
      "bar"

- ``collect``: convert tuple to array

- tuples as function arguments: unpack it use an ellipsis ``f((1, 2, 3)...)`` (Refer to `Varargs Functions <http://julia.readthedocs.org/en/latest/manual/functions/#varargs-functions>`_)
  注：之前的版本还可以使用 ``apply`` 函数，现在该函数已被 Julia 作废。

  .. code:: jlcon

      julia> g() = (1, 2, 3)
      g (generic function with 1 method)

      julia> f(a, b, c) = +(a, b, c)
      f (generic function with 1 method)

      julia> f(g())
      ERROR: MethodError: `f` has no method matching f(::Tuple{Int64,Int64
      ,Int64})
      Closest candidates are:
        f(::Any, ::Any, ::Any)

      julia> f(g()...)
      6

Ranges
--------

- ``1:5``, ``0.0:0.1:10.0``, ``linspace(0.0,10.0,11)``
- convert **Range** to **Array**: ``collect(1:5)`` or simply use ``[1:5]`` (``collect`` is much faster)

Lists
-------

List is one-dimensional array.

- create: ``my_list = ["a", 1, -0.76]``
- access: ``m_list[2]``, ``my_list[end]``, ``my_list[end-1]``
- length: ``length(my_list)``

Vectors
=========

Vectors
---------

- create: ``x=[8,-4,3.5]`` or ``x=[8;-4;3.5]``

  .. math::

     \boldsymbol{x}=\left(
     \begin{array}{c}
     8\\
     -4\\
     3.5
     \end{array}
     \right)

- index: ``x[2]``, ``x[2:3]``, ``x[end]``, ``x[1:2:end]``

- block vectors

  stacked vector: ``a=[b;c]`` (Note: Both :math:`\boldsymbol{b}` and :math:`\boldsymbol{c}` are vectors, so ``a=[b,c]`` does NOT work).

  .. math::

     \boldsymbol{a}=\left(
     \begin{array}{c}
     \boldsymbol{b}\\
     \boldsymbol{c}
     \end{array}
     \right)

- mix vectors with scalars: ``a=[b; 2; c; -6]``

- list with vectors :math:`\boldsymbol{a},\boldsymbol{b},\boldsymbol{c}`: ``vector_list=[a,b,c]``

  * second vector in this list: ``vector_list[2]``
  * access an element in a vector: ``vector_list[2][3]``

- Basic functions for arrays:

  - sum of a vector: ``sum(x)``
  - mean of the entries: ``mean(x)``
  - :math:`\boldsymbol{0}_n` (vector with all entries 0): ``zeros(n)``
  - :math:`\boldsymbol{1}_n` (vector with all entries 1): ``ones(n)``

Vector operations
-------------------

- vector addition and subtraction (the arrays must have the same length): ``+``, ``-``

- scalar-vector addition: ``[2,4,8]+3``

  .. math::

     \left(
     \begin{array}{c}
     2\\
     4\\
     8\\
     \end{array}
     \right)
     + 3 =
     \left(
     \begin{array}{c}
     5\\
     7\\
     11\\
     \end{array}
     \right)

- scalar-vector multiplication: ``-2*[1,9,6]`` or ``[1,9,6]*(-2)``

  .. math::

     -2\,
     \left(
     \begin{array}{c}
     1\\
     9\\
     6\\
     \end{array}
     \right)
     =
     \left(
     \begin{array}{c}
     -2\\
     -18\\
     -12\\
     \end{array}
     \right)

- inner product :math:`\boldsymbol{a}^T\boldsymbol{b}`: ``dot(a,b)`` (:math:`\boldsymbol{a}` and :math:`\boldsymbol{b}` must have the same length)
- vector-vector element-wise operation: ``[2,4].*[10,20]``

Norm and distance
----------------------

- ``norm(x)``

  .. math::

     \left\|\boldsymbol{x}\right\|=\sqrt{x_1^2+x_2^2+\dots+x_n^2}

- ``norm(x-y)``

  .. math::

     \left\|\boldsymbol{x}-\boldsymbol{y}\right\|

- root mean square: ``rms(x)``

  .. math::

     \boldsymbol{x}_{\text{rms}}=\sqrt{\frac{1}{n}\left(x_1^2+x_2^2+\dots+x_n^2\right)}=\frac{\left\|\boldsymbol{x}\right\|}{\sqrt{n}}

- angle between vectors: ``angle_a_b = acos(dot(a,b)/(norm(a)*norm(b)))``

  .. math::

     \angle (\boldsymbol{a},\boldsymbol{b})=\arccos \left(\frac{\boldsymbol{a}^T\boldsymbol{b}}{\left\|\boldsymbol{a}\right\|\left\|\boldsymbol{b}\right\|} \right)


Matrices
=============

Matrics
----------

Matrices are 2D or higher dimensional arrays.

- spaces separate entries in a row; semicolons separate individual rows: ``A=[2 -4 8.2; -5.5 3.5 63]``

  .. math::

     \boldsymbol{A}=
     \left(
     \begin{array}{ccc}
     2 & -4 & 8.2\\
     -5.5 & 3.5 & 63\\
     \end{array}
     \right)

- ``A_rows, A_cols = size(A)``: returns the tuple containing the dimensions of :math:`\boldsymbol{A}`. (``A_rows`` is ``size(A)[1]``, ``A_cols`` is ``size(A)[2]``).

- block matrix: ``X=[A B; C D]`` (:math:`\boldsymbol{A}, \boldsymbol{B}, \boldsymbol{C}` and :math:`\boldsymbol{D}` are matrices)

  .. math::

     \boldsymbol{X}=
     \left(
     \begin{array}{ccc}
     \boldsymbol{A} & \boldsymbol{B}\\
     \boldsymbol{C} & \boldsymbol{D}\\
     \end{array}
     \right)

- useful matrices:

  - :math:`\boldsymbol{0}_{m \times n}` (vector with all entries :math:`0`): ``zeros(m,n)``
  - :math:`\boldsymbol{1}_{m \times n}` (vector with all entries :math:`1`): ``ones(m,n)``
  - :math:`\boldsymbol{I}_{n}` (identity matrix of dimension :math:`n`): ``eye(n)``
  - :math:`\text{diag}(\boldsymbol{x})` (diagonal matrix, :math:`\boldsymbol{x}` is a vector): ``diagm(x)``

Matrix operations
------------------------

- :math:`\boldsymbol{A}^T` (transpose): ``A'``
- matrix addition and subtraction: ``+``, ``-``
- matrix-scalar operations ``+``, ``-``, ``*``, ``/`` apply elementwise: ``10 * [1 2; 3 4]`` gives ``[10 20; 30 40]``
- matrix-vector multiplication ``*``

  For example, ``[1 2; 3 4]*[5, 6]``:

  .. math::

      \left(
      \begin{array}{cc}
      1 & 2\\
      3 & 4\\
      \end{array}
      \right)
      \left(
      \begin{array}{c}
      5\\
      6\\
      \end{array}
      \right)

- ``*`` is also used for matrix-matrix multiplication
- ``*.`` is for matrix-matrix element-wise multiplication

Useful functions
-------------------

- sum of all entries of a matrix: ``sum(A)``
- average of entries of a matrix: ``mean(A)``
- Element-wise *max* and *min*: ``max(A, B)``, ``min(A, B)`` (the arguments must have the same size unless one is a scalar)
- ``norm(A[:])`` or ``vecnorm(A)`` means :math:`\left(\sum_{i,j} A_{i,j}^2\right)^{1/2}` (Note that ``norm(A)`` has a different meaning and do not misuse it)

Tricks
==========

For loops
-----------

- loop over a **Range**

  .. code:: julia

     value = 0
     for i in 1:10
       value += i
     end

- loop over a **List**

  .. code:: julia

     value = 0
     my_list = [1,2,3,4,5]
     for i in my_list
       value += i
     end

- ``zip``:

  .. code:: julia

      countries = ("Japan", "Korea", "China")
      cities = ("Tokyo", "Seoul", "Beijing")
      for (country, city) in zip(countries, cities)
       println("The capital of $country is $city")
      end

- ``enumerate``: yields a tuple ``(index, value)``

  .. code:: julia

      countries = ("Japan", "Korea", "China")
      cities = ("Tokyo", "Seoul", "Beijing")
      for (i, country) in enumerate(countries)
          city = cities[i]
          println("The capital of $country is $city")
      end




Initialization
----------------

Data types
^^^^^^^^^^^^

List (1D **Array**) and matrix (2D or higher dimensional **Array**) may include entries of different types: ``[1, "2", sin, 3.0]``, ``[1, "2"; sin, 3.0]``

.. code:: jlcon

    julia> [1, "2", sin, 3.0]
    4-element Array{Any,1}:
     1
     "2"
     sin
     3.0

    julia> [1 "2"; sin 3.0]
    2x2 Array{Any,2}:
     1      "2"
     sin    3.0

如果元素类型只有常用的数学类型的时候，会按 ``Int64``, ``Rational{Int64}``, ``Float64`` 的顺序进行自动的promotion.
如果元素中有复数，则其余实数类型也会被自动转换为复数，实部和复部类型按之前的顺序自动promotion.

例子如下：

.. code:: jlcon

   julia> [2, 3//4]
   2-element Array{Rational{Int64},1}:
    2//1
    3//4

   julia> [2, 3//4, 0.1]
   3-element Array{Float64,1}:
    2.0
    0.75
    0.1

   julia> [2, 3//4, 0.1, 1+2im]
   4-element Array{Complex{Float64},1}:
     2.0+0.0im
     0.75+0.0im
     0.1+0.0im
     1.0+2.0im

然而，list 或 matrix 的类型也可以进行明确指定。如：

.. code:: jlcon

    julia> Float64[1,2,3]
    3-element Array{Float64,1}:
     1.0
     2.0
     3.0

Empty array
^^^^^^^^^^^^^^

Initialize an empty array. List example (1D array):

.. code:: jlcon

    julia> Float64[]
    0-element Array{Float64,1}

    julia> Array(Float64,0)
    0-element Array{Float64,1}

    julia> Array{Float64}(0)
    0-element Array{Float64,1}

    julia> []
    0-element Array{Any,1}

Matrix example (2D or higher dimensional array), 初始化某一维度为0:

.. code:: jlcon

    julia> Array(Float64,0,2)
    0x2 Array{Float64,2}

    julia> Array{Float64}(0,2)
    0x2 Array{Float64,2}

也可以用 ``reshape`` 函数实现同样效果：

.. code:: jlcon

    julia> reshape([],0,2)
    0x2 Array{Any,2}

Allocate array (no initialization)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- List

  Allocate a list (1D array), and fill it with random values:

  - 直接使用构造函数 ``Array``

    .. code:: jlcon

        julia> Array(Float64,3)
        3-element Array{Float64,1}:
         1.08099e-314
         1.08097e-314
         1.08098e-314

        julia> Array{Float64}(3)
        3-element Array{Float64,1}:
         0.0
         1.061e-314
         0.0

  - 基于另一个 list, 创建与之相同类型的 list, 利用函数 ``similar``

    .. code:: jlcon

       julia> similar([1.0, 2.0, 3.0])
       3-element Array{Float64,1}:
        1.0818e-314
        1.08225e-314
        1.08853e-314

  - 如果数据类型为 Any, 则会被填充未知量。

    .. code:: jlcon

      julia> Array{Any}(3)
      3-element Array{Any,1}:
       #undef
       #undef
       #undef

    当然也等同于使用 ``Array(Any,3)``.

- Matrix

  - 同理，我们也可以创建一个 2x3 矩阵（元素为随机产生）： ``Array(Float64,2,3)`` or ``Array{Float64}(2,3)`` or ``similar([1 2 3; 4 5 6])``

  - 为方便起见，一维和二维的情况下，Julia提供了两个函数, ``Vector(3)``, ``Matrix(2,3)`` 分别相当于 ``Array(Any,3)`` 以及 ``Array(Any,2,3)``.

Initialize a matrix
^^^^^^^^^^^^^^^^^^^^^

创建一个 2x3 矩阵并赋值，可以用下列方式：

1. 按行创建

   .. code:: jlcon

      julia> [1 2 3; 4 5 6]
      2x3 Array{Int64,2}:
       1  2  3
       4  5  6

#. 按列创建

   .. code:: jlcon

      julia> [[1, 4] [2, 5] [3, 6]]
      2x3 Array{Int64,2}:
       1  2  3
       4  5  6

#. 由另一个 list 或 matrix 变形而来

   .. code:: jlcon

      julia> reshape([1,4,2,5,3,6], 2, 3)
      2x3 Array{Int64,2}:
       1  2  3
       4  5  6

.. note:: Julia 是 **列主序** (Column-major)

   * Column-major order: Julia, Fortran, R, Matlab, GNU Octave, BLAS, LAPACK, OpenGL/OpenGL ES
   * Row-major order: C/C++, Mathematica, Pascal, Python, C#/CLI/.Net, Direct3D

由上面 ``reshape`` 结果也可以看出 Julia 是列主序(Column-major)的。而高维矩阵也可以看成等效的一维矩阵，
比如 ``A = [1 2 3; 4 5 6]``, 那么 ``A[4]`` 等于 :math:`4` 而非 :math:`5`.
因此也可以使用 ``A[:]`` 得到矩阵转换为一维数组的结果。在用多维和一维这两种不同方式表示时，有两个函数很有用：

- ``ind2sub(dims, index)`` 求一维数组表示法中的 index 元素在多维表示法中的位置。
  如 ``ind2sub((2,3), 4)`` 返回 ``(2,2)``, 意即在一个 ``2x3`` 维的矩阵中，位置 ``(2,2)`` 对应一维数组中的脚标 ``4``
- ``sub2ind((2,3), 2,2)`` 返回 ``4``, 表示在 ``2x3`` 的矩阵中位置 ``(2,2)`` 对应一维数组中的第 ``4`` 个位置。


Useful functions
-----------------

.. note:: 参考

   1. http://docs.julialang.org/en/stable/stdlib/arrays/
   #. http://docs.julialang.org/en/stable/stdlib/collections/
   #. https://en.wikibooks.org/wiki/Introducing_Julia/Arrays_and_tuples

基本信息
^^^^^^^^^^^^^

以 ``exampleArray = [1 2 3; 4 5 6; 7 8 9]`` 为例：

- ``ndims(exampleArray)`` 返回维度 ``2``
- ``size(exampleArray)`` 返回各维大小 ``(3,3)``
- ``length(exampleArray)`` 返回总元素数量 ``9``

最大(小)值，以及求和
^^^^^^^^^^^^^^^^^^^^^^^^

- ``maximum``, ``minimum`` 求list或矩阵(及其某一维度上)的最大值和最小值
- ``maxabs``, ``minabs``, 绝对值的最大(小)值
- ``findmax``, ``findmin`` 会返回一个tuple，``(value, index)``，即包括最大（小）值及其位置
- ``sum``, 求和
- ``sumabs``, 求绝对值之和
- ``sumabs2``, 求平方和，等同于 ``sum(abs2(itr))``


查找，筛选
^^^^^^^^^^^^^^^^^^

- ``in`` 判断元素是否属于某array，如 ``in(3, 1:10)`` 会返回 ``true``
- ``count(predicate, A)`` 返回所有满足 ``predicate`` 的元素数量. 如 ``count(isodd, exampleArray)`` 返回 ``5``.
- ``find(predicate, A)`` Return a vector of the linear indexes of ``A`` where ``predicate`` returns ``true``.

  .. code:: jlcon

      julia> find(iseven,1:10)
      5-element Array{Int64,1}:
      2
      4
      6
      8
      10

  如果找不到，则会返回 ``0``. 常用的内置判断函数有 ``iseven``, ``isodd``, ``isinteger``, ``isreal``, ``isprime``, 还可以用 lambda 表达式自定义函数。

- ``findfirst`` 常用用法 (``findlast`` 用法类似)：

  - ``findfirst(A)`` Return the index of the first non-zero value in ``A`` (determined by ``A[i]!=0``).
  - ``findfirst(A,v)`` Return the index of the first element equal to ``v`` in ``A``. 如 ``findfirst(2:2:10, 6)`` 返回 ``3``.
  - ``findfirst(predicate, A)`` Return the index of the first element of ``A`` for which predicate returns ``true``. 如 ``findfirst(isprime, 0:10)`` 返回 ``3``.

- ``findnext`` 与 ``findfirst`` 相似，但提供一个额外的参数表示搜索开始位置。所以 ``findfirst(predicate, A)`` 相当于 ``findnext(predicate, A, 1)``

  还有一个相似的函数 ``findprev``.

  注意，``find``, ``findfirst``, ``findlast`` 返回的值都是 index，因此想要拿到对应的值就应该用 ``A[findfirst(predicate,A)]`` 类似的形式。

- ``filter`` 与 ``find`` 作用相似，不同点是 ``filter`` 直接返回的是元素值而 ``find`` 返回的是对应的脚标。同时 ``filter!`` 可以直接将原来的array改变，只保留满足条件的值。
- 使用 broadcasting 与 indexing. 如 ``A[A.>4]`` 与 ``filter(x->x>4, A)`` 作用相同; ``A[isodd.(A)]`` 与 ``filter(isodd, A)`` 作用相同 (``isodd.(A)`` 这种写法仅Julia 0.5版本之后支持).
  注意，``A[A%3.==0]`` 是正确写法而 ``A[A.%3==0]`` 是不正确的。(实践发现当 ``A`` 元素比较多时，0.4版本这种方式比 ``filter`` 要更快一些。但在另一机器上0.5版本测试结果各有胜负)
- ``any(predicate, A)``: 只要 ``A`` 中存在一个元素满足条件就返回 ``true``
- ``all(predicate, A)``: 只有 ``A`` 中所有元素都满足条件就返回 ``true``

删除行或列
^^^^^^^^^^^^^^^^

假设一个 3x3 的矩阵 ``A``, 我们要删除其第二行变成一个 2x3 矩阵。在Julia中，没有办法直接删除元素来改变原矩阵内容，即 ``A[2,:]=[]`` 类似这样的做法是无效的。
因此我们只能复制原矩阵中部分值赋值给新的矩阵。使用之前提到的用 predicate 函数来indexing的方法，取出剩余部分赋值给新的矩阵 ``B``.
即 ``B=A[1:end.!=2,:]``

Joining arrays and matrices
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``[A B]`` or ``hcat(A, B)``
- ``[A; B]`` or ``vcat(A, B)``
- ``[A B; C D]``
- ``vec(A)`` 把 ``A`` 变成一维数组

Array of arrays
------------------

- 基本例子：

  .. code:: jlcon

      julia> Array[1:3, 4:6]
      2-element Array{Array{T,N},1}:
       [1,2,3]
       [4,5,6]

      julia> Array[[1,2], [3,4]]
      2-element Array{Array{T,N},1}:
       [1,2]
       [3,4]

- Create an empty array of arrays:

  .. code:: jlcon

      julia> Array{Int}[]
      0-element Array{Array{Int64,N},1}

      julia> Array{Int, 2}[]
      0-element Array{Array{Int64,2},1}

      julia> Array(Array{Float64,3},0)
      0-element Array{Array{Float64,3},1}

- Create by specifying the size:

  .. code:: jlcon

      julia> Array(Array{Int64, 2},3)
      3-element Array{Array{Int64,2},1}:
       #undef
       #undef
       #undef

      julia> Array{Array{Int64, 2}}(3)
      3-element Array{Array{Int64,2},1}:
       #undef
       #undef
       #undef

- Use ``hcat()`` or ``vcat()`` to convert an array to a matrix (Refer to `slurping and splatting <http://docs.julialang.org/en/stable/manual/faq/#what-does-the-operator-do>`_)

  .. code:: jlcon

      julia> a = Array[[1,2],[3,4],[5,6]]
      3-element Array{Array{T,N},1}:
       [1,2]
       [3,4]
       [5,6]

      julia> hcat(a...)
      2x3 Array{Int64,2}:
       1  3  5
       2  4  6

      julia> vcat(a...)
      6-element Array{Int64,1}:
       1
       2
       3
       4
       5
       6

      julia> b = Array[[1 2],[3 4],[5 6]]
      3-element Array{Array{T,N},1}:
       1x2 Array{Int64,2}:
       1  2
       1x2 Array{Int64,2}:
       3  4
       1x2 Array{Int64,2}:
       5  6

      julia> vcat(b...)
      3x2 Array{Int64,2}:
       1  2
       3  4
       5  6

      julia> hcat(b...)
      1x6 Array{Int64,2}:
       1  2  3  4  5  6

Performance
===============

参考 `Reddit Link <https://www.reddit.com/r/Julia/comments/3vhv8l/neat_little_speed_comparison_between_forloops_and/>`_ 中的写法
以及 `Performance Tips <http://docs.julialang.org/en/stable/manual/performance-tips/>`_, 在比较运行效率时，最好把例子都写进同一个函数。

List comprehension vs ``for`` loop vs ``map``
-------------------------------------------------

.. code:: julia

   function test_loop()
       atest = rand(1000)
       btest = rand(30000)

       tic()
       list1 = [count(x-> v >=x, atest) for v in btest]
       list_untyped = toq()

       tic()
       list2 = Int64[count(x-> v >=x, atest) for v in btest]
       list_typed = toq()

       tic()
       len = length(btest)
       list3 = Array(Int64, len)
       for i in 1:len
           list3[i]=count(x-> btest[i] >=x, atest)
       end
       forloop = toq()

       tic()
       list4 = map(v->count(x-> v >=x, atest), btest)
       mapfun = toq()

       print("
       list_untyped: $list_untyped
       list_typed: $list_typed
       forloop: $forloop
       mapfun: $mapfun
       ")
   end


下面是 Julia 0.4.7 运行第二次的结果（第一次结果未编绎不准确，故不能用作标准）, 0.5 版本结果一致。因此这种情况下 ``map`` 要稍快一些。

.. code:: jlcon

   julia> test_loop()

     list_untyped: 0.848853296
     list_typed: 0.875462525
     forloop: 1.561129306
     mapfun: 0.836571566


``findlast`` faster than ``count``
---------------------------------------

例子：两个 array (大小可能不同), ``A`` 和 ``B``, 现在需要找出 ``B`` 中每个元素落在 ``A`` 的哪个区间，比如 ``A = [1,3,5,7]``, ``B = [1.2,5.5]``,
则会返回 ``B`` 中每个元素在 ``A`` 中的相应位置 ``1`` (即 ``1.2`` 属于区间 ``[1,3]``) 和 ``3`` (``5.5`` 属于区间 ``[5,7]``). Mathematica 中可以使用 ``LengthWhile`` 来做，
Julia 中有两个函数可以完成: ``findlast`` (定义在 "array.jl" 中) 与 ``count`` (定义在 "reduce.jl" 中)，而经多次测试，前者更快且使用的内存更少。

.. code:: julia

   function test_findlast_count()
       atest = rand(1000)
       btest = rand(30000)

       tic()
       list1 = Int64[findlast(x-> v >=x, atest) for v in btest]
       findlast_time = toq()

       tic()
       list2 = Int64[count(x-> v >=x, atest) for v in btest]
       count_time = toq()

       print("
       findlast_time: $findlast_time
       count_time: $count_time
       ")
   end

.. code:: jlcon

   julia> test_findlast_count()

     findlast_time: 0.002317571
     count_time: 0.866425052

关于求最值
--------------

- single array: ``for`` loop vs ``maximum``

  ``maximum()`` is faster.

  .. code:: julia

     function test_singarray_max()
         arr = rand(100000000)

         tic()
         max_arr = 0.0
         for x in arr
             if max_arr < x
                 max_arr = x
             end
         end
         single_array_forloop = toq()

         tic()
         max_arr2 = maximum(arr)
         single_array_maximum = toq()

         print("
         single_array_forloop: $single_array_forloop
         single_array_maximum: $single_array_maximum
         ")
     end

  .. code:: jlcon

     julia> test_singarray_max()

       single_array_forloop: 0.177215175
       single_array_maximum: 0.077552238

- multiple arrays: different versions of ``for`` loop vs ``maximum``

  ``for`` loop using indexing is the fatest.

  .. code:: julia

     function test_multiarray_max()
         arr1=rand(100000000)
         arr2=rand(100000000)

         tic()
         max_arr = 0.0
         for x in arr1-arr2 # a temporary array arr1-arr2 is generated here
             if max_arr < x
                 max_arr = x
             end
         end
         multiarray_forloop_temp = toq()

         tic()
         max_arr = 0.0
         for i in 1:length(arr1)
             temp = arr1[i] - arr2[i]
             if max_arr < temp
                 max_arr = temp
             end
         end
         multiarray_forloop_index = toq()

         tic()
         max_arr = 0.0
         for (a,b) in zip(arr1,arr2)
             temp = a-b
             if max_arr < temp
                 max_arr = temp
             end
         end
         multiarray_forloop_zip = toq()

         tic()
         list = maximum(arr1-arr2)
         multiarray_maximum = toq()

         print("
         multiarray_forloop_temp: $multiarray_forloop_temp
         multiarray_forloop_index: $multiarray_forloop_index
         multiarray_forloop_zip: $multiarray_forloop_zip
         multiarray_maximum: $multiarray_maximum
         ")
     end

  .. code:: jlcon

     julia> test_multiarray_max()

       multiarray_forloop_temp: 0.434184324
       multiarray_forloop_index: 0.161199946
       multiarray_forloop_zip: 0.206321564
       multiarray_maximum: 0.446215882
