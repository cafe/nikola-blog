.. title: Arc Length Reparameterization
.. slug: arc-length-reparameterization
.. date: 2016-06-28 10:04:59 UTC+08:00
.. tags: algorithm, mathjax
.. category: math
.. link: 
.. description: 
.. type: text
.. author: YONG

reference: https://services.math.duke.edu/~wka/math103/curvature.pdf

Suppose :math:`I` is an interval and :math:`\mathbf{r} : I \mapsto \mathbb{R}^n` is a curve in :math:`\mathbb{R}^n` whose speed is never zero. Suppose :math:`t_0 \in I` and let

.. math::
    
    \sigma (t) = \int_{t_0}^t \| \vec{r}' (\tau) \| d\tau

.. TEASER_END

Given a vector function :math:`\vec{r}(t)`, its arc length from :math:`t = a` to :math:`t = b` is

.. math::
    
    L = \int_a^b \| \vec{r}' (t)\| dt

Replacing :math:`b` with :math:`u`, the arc length function is

.. math::
    
    s(u) = \int_a^u \| \vec{r}' (\tau) \| d\tau


