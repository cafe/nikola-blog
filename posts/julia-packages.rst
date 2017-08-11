.. title: Julia Packages
.. slug: julia-packages
.. date: 2017-03-18 09:05:10 UTC+08:00
.. tags: julia
.. category: programming
.. link:
.. description:
.. type: text

.. sectnum::

.. contents::

.. TEASER_END

Commands
==================

- ``Pkg.update()`` Update the package database
- ``Pkg.status()`` List the information of all installed packages
- ``Pkg.resolve()`` Let Julia resolve package dependencies automatically
- ``Pkg.add("HDF5")`` Install package ``HDF5``
- ``using HDF5`` Include the package ``HDF5`` in the current file


Packages I Am Using
======================

BenchmarkTools
-------------------

A benchmarking framework for the Julia language `GitHub <https://github.com/JuliaCI/BenchmarkTools.jl>`__

- ``@btime sin(1)`` Print the minimum time and memory allocation before returning the value of the expression ``sin(1)``
- ``@belapsed sin(1)`` Simplified version of ``@time``, only print the minimum time (unit: second)
- ``@benchmark sin(1)`` Full version of ``@btime``, print all the information of the benchmarking

HDF5
---------

Saving and loading data in the HDF5 file format `GitHub <https://github.com/JuliaIO/HDF5.jl>`__

- ``h5write("filename.h5", "/nameA", A)`` Write array ``A`` to a dataset named "nameA" inside the root group. Use "mygroup/nameA" to write data inside "mygroup"
- ``B = h5read("filename.h5", "/nameA")`` Read dataset "nameA" and set the value to ``B``.

  .. code:: julia

     if isfile("filename.h5") # if the file already exists, delete it
         rm("filename.h5")
     end
     h5write("filename.h5", "/nameA", A) # write
     B = h5read("filename.h5", "/nameA") # read

PyPlot
-------------

Plotting for Julia based on matplotlib.pyplot `GitHub <https://github.com/JuliaPy/PyPlot.jl>`__

- ``plot(Xdata, Ydata, ".")``
- ``plot(Xdata, Ydata, color="red", linewidth=2.0, linestyle="--")``
- ``title("A sinusoidally modulated sinusoid")``


Useful Packages
=====================

`JuliaPro <https://juliacomputing.com/products/juliapro.html>`__ provides a list of commonly used packages:

General programming
-----------------------

- DataStructures `GitHub <https://github.com/JuliaLang/DataStructures.jl>`__
- LightGraphs `GitHub <https://github.com/JuliaGraphs/LightGraphs.jl>`__

General Math
----------------

- Calculus `GitHub <https://github.com/johnmyleswhite/Calculus.jl>`__
- DataFrames `GitHub <https://github.com/JuliaStats/DataFrames.jl>`__
- StatsBase `GitHub <https://github.com/JuliaStats/StatsBase.jl>`__
- Distributions `GitHub <https://github.com/JuliaStats/Distributions.jl>`__
- HypothesisTests `GitHub <https://github.com/JuliaStats/HypothesisTests.jl>`__
- GLM `GitHub <https://github.com/JuliaStats/GLM.jl>`__

Optimization
----------------

- JuMP `GitHub <https://github.com/JuliaOpt/JuMP.jl>`__
- Optim `GitHub <https://github.com/JuliaOpt/Optim.jl>`__
- Roots `GitHub <https://github.com/JuliaMath/Roots.jl>`__

Databases
-------------

- ODBC `GitHub <https://github.com/JuliaDB/ODBC.jl>`__
- JDBC `GitHub <https://github.com/JuliaDB/JDBC.jl>`__

Building UIs and Visualization
----------------------------------

- Gadfly `GitHub <https://github.com/GiovineItalia/Gadfly.jl>`__
- PyPlot `GitHub <https://github.com/JuliaPy/PyPlot.jl>`__
- Interact `GitHub <https://github.com/JuliaGizmos/Interact.jl>`__

Deep Learning and Machine Learning
---------------------------------------

- Mocha `GitHub <https://github.com/pluskid/Mocha.jl>`__
- MXNet `GitHub <https://github.com/dmlc/MXNet.jl>`__
- Knet `GitHub <https://github.com/denizyuret/Knet.jl>`__
- Clustering `GitHub <https://github.com/JuliaStats/Clustering.jl>`__
- DecisionTree `GitHub <https://github.com/bensadeghi/DecisionTree.jl>`__

Interoperability with other languages
-----------------------------------------

- RCall `GitHub <https://github.com/JuliaInterop/RCall.jl>`__
- JavaCall `GitHub <https://github.com/JuliaInterop/JavaCall.jl>`__
- PyCall `GitHub <https://github.com/JuliaPy/PyCall.jl>`__

File and data formats
--------------------------

- JSON `GitHub <https://github.com/JuliaIO/JSON.jl>`__
- HDF5 `GitHub <https://github.com/JuliaIO/HDF5.jl>`__
- JLD `GitHub <https://github.com/JuliaIO/JLD.jl>`__

Economics and Finance
-------------------------

- QuantEcon `GitHub <https://github.com/QuantEcon/QuantEcon.jl>`__
