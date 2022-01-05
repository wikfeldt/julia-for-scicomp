Developing in Julia
===================

.. questions::

   - How do modules work in Julia?
   - How do I create a new project?
   - How can I create reprodubible environments?
   - How are tests written in Julia?
   - How does scoping work?
     
.. objectives::

   - Get familiar with the package manager
   - Learn to use, extend and write packages in Julia
   - Learn how to create reproducible environments and add tests to your code
   - Understand scoping in Julia
     

Julia's package manager
-----------------------

Julia comes with an powerful inbuilt package manager. We can 
also use the package manager to manage isolated environments 
and dependencies.

- To enter the package manager from a Julia session we 
  can hit the ``]`` character, after which the prompt 
  changes to ```pkg>```. 
- To see all available options, type `help`. For example, we can 
  install a new package by ``pkg> add some-package``.
- To go back to the REPL, hit backspace or ``^C``.

.. callout:: Using the ``Pkg`` module

   Instead of using ``]`` to enter the package manager, this lesson 
   will use the following syntax to manage packages. This way, code blocks
   can be copied directly into the REPL and executed:

   .. code-block:: julia

      using Pkg
      Pkg.add("some-package")
      Pkg.status()

Let us get familiar with the package manager by working with an 
example package that ships with Julia.
To add the `Example` package

Dependencies
^^^^^^^^^^^^


Creating a new project
----------------------



Modules
^^^^^^^



Where can I find existing packages?
-----------------------------------



Adding tests
------------

- Test
- ReTest
- InlineTest

**Should be installed in default environment, not in project**.
VSCode imports it with the julia extension.


  
See also
--------

- https://docs.julialang.org/en/v1/manual/faq/#Packages-and-Modules
- https://docs.julialang.org/en/v1/manual/code-loading/#Federation-of-packages
- https://julialang.github.io/Pkg.jl/v1/creating-packages/  
- https://juliahub.com/ui/Home
- https://discourse.julialang.org/t/experimental-reproducibility-julia-vs-the-rest/46769/6
- https://julialang.github.io/Pkg.jl/v1/environments/
- https://docs.julialang.org/en/v1.0/stdlib/Pkg/
     
