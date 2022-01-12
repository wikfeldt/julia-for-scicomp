Distributed computing
=====================

.. questions::

   - How can I parallelise over multiple cores and nodes?

.. objectives::

   - Understand the difference between the available parallelization mechanisms in Distributed.jl
   - Know when you can use ``@distributed`` and ``pmap``
   - Learn to work with SharedArrays and Distributed arrays


Overview
--------

WRITEME: General discussion

- MPI.jl
- Distributed.jl
- Kubernetes.jl
- ClusterManagers

.. code-block::
   
   function throw_darts(N)
       n = 0
       for i in 1:N
           if rand()^2 + rand()^2 < 1
           n += 1
           end
       end
       return n
   end

.. code-block::

   function estimate_pi(N, loops)
       n = sum(pmap((x)->darts_in_circle(N), 1:loops))
       return 4 * n / (loops * N)
   end


@distributed
------------


``pmap``
--------


SharedArrays
------------


DistributedArrays
-----------------

notes
-----

example function to distribute:

.. code-block:: julia

   @everywhere function compute_pi(N)
      series = 1.0
      for i in 1:N
         series += (isodd(i) ? -1 : 1) / (2i + 1)
      end
      return 4*series
   end

**From Julia-Academy:**
Structure your algorithms and use a distributed mechanism that fits with the 
time and memory parameters of your problem

- @distributed can be good for reductions and even relatively fast inner loops with limited (or no) explicit data transfer
- pmap is great for very expensive inner loops that return a value
- SharedArrays can be an easier drop-in replacement for threading-like behaviors (on a single machine)
- DistributedArrays can turn the problem on its head and let the data do the work splitting!



Exercises
---------

.. exercise:: Using SharedArrays with Heatequation

   Open up the Heatequation.jl package in VSCode and read the "SharedArrayHint"
   comments. Think about what you should do, and then try doing it.
   After you're done, benchmark a few test runs. 

   .. solution:: 

      Switch to the `SharedArrays` branch of the repository (``git checkout SharedArrays``)
      and have a look at the code.

.. exercise:: Using DistributedArrays with Heatequation

   Open up the Heatequation.jl package in VSCode and read the "DistributedArrayHint"
   comments. Think about what you should do, and then try doing it.
   After you're done, benchmark a few test runs.

   .. solution:: 

      Switch to the `DistributedArrays` branch of the repository (``git checkout DistributedArrays``)
      and have a look at the code.


See also
--------

- https://docs.julialang.org/en/v1/manual/distributed-computing/
