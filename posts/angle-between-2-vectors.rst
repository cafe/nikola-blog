.. title: Angle between 2 Vectors
.. slug: angle-between-2-vectors
.. date: 2016-04-26 01:34:15 UTC+08:00
.. tags: algorithm
.. category: programming
.. link: 
.. description: 
.. type: text
.. author: YONG

两向量夹角问题
--------------

Given two vectors v1(x1,y1), v2(x2,y2) and they are not necessarily
normalized, compute the angle beta between v1 and v2.

.. TEASER_END

通常做法
--------

A common way is using dot product (C++ version):

.. code:: cpp

    beta = acos((x1 * x2 + y1 * y2) / sqrt((x1*x1 + y1*y1)*(x2*x2 + y2*y2)))

The resulting beta is within [0, Pi]. It is equivalent to using
``VectorAngle[]`` function in *Mathmatica*. However, it seems
inefficient due to the ``acos()`` and ``sqrt()`` function. Moreover, we
lost the information of the sign of the angle.

改进
----

We can use ``atan2()`` function instead:

.. code:: cpp

    beta = atan2(x1*y2 - y1*x2, x1*x2 + y1*y2)

The obtained beta is in range [-Pi, Pi].

完整代码
--------

Source: `Vector
Angle <http://referencesource.microsoft.com/#WindowsBase/Base/System/Windows/Vector.cs,102>`__

.. code:: csharp

    /// <summary>        
    /// AngleBetween - the angle between 2 vectors        
    /// </summary>        
    /// <returns>        
    /// Returns the the angle in degrees between vector1 and vector2        
    /// </returns>        
    /// <param name="vector1"> The first Vector </param>
    /// <param name="vector2"> The second Vector</param>        
    public static double AngleBetween(Vector vector1, Vector vector2)
    {            
    double sin = vector1._x * vector2._y - vector2._x * vector1._y;             
    double cos = vector1._x * vector2._x + vector1._y * vector2._y;             
    return Math.Atan2(sin, cos) * (180 / Math.PI);        
    }

Since the ``atan2()`` function in C++ is the same with the C# version:
``atan2(y, x)``. Notice that in *Mathematica*, ``ArcTan[]`` can take 2
arguments like ``atan2()``, but in a different order: ``ArcTan[x, y]``.

