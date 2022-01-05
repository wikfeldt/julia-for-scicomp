Distributed computing
=====================

.. questions::

   - How can I parallelise over multiple cores and nodes?

.. objectives::

   - Learn to use the Distributed package
   - Get familiar with how to use MPI in Julia


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

Section
-------


See also
--------

- https://docs.julialang.org/en/v1/manual/distributed-computing/
