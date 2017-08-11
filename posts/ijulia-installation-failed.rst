.. title: IJulia Installation Failed
.. slug: ijulia-installation-failed
.. date: 2017-03-19 13:04:52 UTC+08:00
.. tags: julia
.. category: programming
.. link:
.. description:
.. type: text

"IJulia" is the Julia version of "Jupyter". It works with plotting packages like "Gadfly" and "PyPlot".
It shows failure information related to "WinRPM" when installing "IJulia".

Environment: Julia 0.5.1 x64 on Windows 10

.. TEASER_END

Output
=================================

Output after running ``Pkg.add("IJulia")`` or ``Pkg.build("IJulia")``:

::

		INFO: Downloading https://cache.julialang.org/http://download.opensuse.org/repositories/windows:/mingw:/win64/openSUSE_42.2/repodata/repomd.xml
		WARNING: Unknown download failure, error code: 2148270088
		WARNING: Retry 1/5 downloading:
		...
		WARNING: Retry 5/5 downloading: https://cache.julialang.org/http://download.opensuse.org/repositories/windows:/mingw:/win64/openSUSE_42.2/repodata/repomd.xml
		WARNING: received error 0 while downloading https://cache.julialang.org/http://download.opensuse.org/repositories/windows:/mingw:/win64/openSUSE_42.2/repodata/repomd.xml

Solution
==============

1. Go to ``D:\home\.julia\v0.5\WinRPM\sources.list``
#. Delete ``https://cache.julialang.org/`` at the beginning of the two entries and save the changes.
#. Run ``Pkg.build("IJulia")``
