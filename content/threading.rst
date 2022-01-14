Multi-threading
===============

.. questions::

   - How do I benchmark Julia code?
   - How does threading work in Julia?

.. objectives::

   - Learn to use BenchmarkTools
   - Learn to use ``Threads.@thread``


Introducing Heatequation
------------------------

We will need a realistic Julia package to work on for all remaining exercises.
For this purpose we will use a minimal heat equation solver, inspired by 
`this educational repository containing C/C++ versions with different 
parallelization strategies <https://github.com/cschpc/heat-equation>`_ (credits to 
CSC Finland). The Julia version of this package can be found at 
https://github.com/enccs/heatequation.jl but the source files are also displayed 
below.

.. tabs:: 

   .. tab:: Heatequation.jl

      .. literalinclude:: code/Heatequation/src/Heatequation.jl
         :language: julia

   .. tab:: setup.jl

      .. literalinclude:: code/Heatequation/src/setup.jl
         :language: julia

   .. tab:: io.jl

      .. literalinclude:: code/Heatequation/src/io.jl
         :language: julia

   .. tab:: core.jl

      .. literalinclude:: code/Heatequation/src/core.jl
         :language: julia

   .. tab:: Project.toml

      .. literalinclude:: code/Heatequation/Project.toml
         :language: julia         


Benchmarking
------------

Base Julia already has the ``@time`` macro to print the time it takes to 
execute an expression. However, to get more accurate values it is better to 
rely on the `BenchmarkTools.jl <https://juliaci.github.io/BenchmarkTools.jl/dev/manual/>`_ 
framework, which provides convenient macros to perform benchmarking:

- ``@btime``: for quick sanity checks, prints the time an expression takes and the memory allocated 
- ``@benchmark``: runs a fuller benchmark on a given expression.

As with `Revise.jl` and `Test.jl`, `BenchmarkTools.jl` should be installed in the base environment:

.. code-block::

   Pkg.activate()
   Pkg.add("BenchmarkTools")

Let us try it out on the Heatequation package in the REPL. 
We could use the ``Pkg.develop()`` function to clone the repository 
into our `~/.julia/dev` folder, which is a good way to work on existing 
Julia packages. Here, we instead imagine that we wrote this package and it 
exists on our computer, so we start by cloning the repository (or download and 
unpack a zip archive) to a new folder:

.. code-block:: shell

   cd $HOME/julia
   git clone https://github.com/wikfeldt/Heatequation.jl
   cd Heatequation

Next open a new VSCode window and navigate to the new directory. 
Open up a Julia REPL and activate the `HeatEquation` environment.

When everything has been set up, we can import `HeatEquation` and start 
benchmarking. We should also not forget to import `Revise`!

.. code-block:: julia

   using HeatEquation
   using Revise
   using BenchmarkTools

   @benchmark simulate(1000, 1000, 500)

We can also capture the output of ``@benchmark``:

.. code-block:: julia

   bench_results = @benchmark simulate(1000, 1000, 500)
   typeof(bench_results)
   println(minimum(bench_results.times))


Profiling
---------

.. code-block:: julia

   using Profile
   Profile.clear()

   @profile simulate(1000, 1000, 500)
   Profile.print(maxdepth=15)

Optimization options
--------------------

@inbounds
^^^^^^^^^

@simd
^^^^^




See also
--------

- https://docs.julialang.org/en/v1/manual/multi-threading/
- https://julialang.org/blog/2019/07/multithreading/
