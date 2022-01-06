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
     

Tooling
-------




Structure of a Julia package
----------------------------

Code written in Julia is normally encapsulated in modules which 
in turn are made available as a package that can be included in other 
projects. 
All functions, variables and custom types can be put in one 
(possibly large) module file with the same name as the module, 
or (more commonly) into multiple files
according to the functionality (``core.jl``, ``io.jl``, ``utilities.jl``, ...).
In the latter case, there is still one file with the name of the module 
where the other files are imported, and the module's API is defined by 
exported functions and types.

- Look at a good example module here

Modules are imported by either the ``using`` or ``import`` keywords.
They work very similarly, the difference is how variables 
defined in the module are brought into scope:

- With ``using ModuleName``, all `exported` names (variables and functions) in the 
  module are brought into scope
- With ``import ModuleName``, the module's names need to be qualified, e.g. 
  ``ModuleName.func()`` or ``ModuleName.var1``.

To concretize Let us put the code we wrote in the previous episode into a 
module called `Points`, and then discuss the consequences of 
doing so.

.. code-block:: julia



-  look at a largish Julia package
-  discuss scope and its rules


Julia's package manager
-----------------------

Julia comes with an powerful inbuilt package manager to install 
and remove packages, manage dependencies and create isolated 
software environments.

.. type-along:: Entering the package manager
   
   - To enter the package manager from a Julia session we 
     can hit the ``]`` character, after which the prompt 
     changes to ```pkg>```. 
   - To see all available options, type `help`. For example, we see that to 
     install a new package we should type ``pkg> add some-package``.
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

Environments
^^^^^^^^^^^^

It is good practice to develop software in isolated environments.
This enables us to use different versions of packages for different 
projects and avoids dependency clashes. It is also the best way to 
ensure `reproducibility` because the exact same software environment 
can be easily created on different computers.

We begin by creating a new environment:

.. code-block:: julia

   Pkg.activate("example-project")

The output tells us that a new environment has been created in our 
current directory - specifically using the ``Project.toml`` file.

We now add the `Example` package by

.. code-block:: julia

   Pkg.add("Example")
   Pkg.status()

The status command shows the version of the `Example` package installed in 
our new ``Project.toml`` file.  
What does this file contain? Try printing it through the Julia shell by 
typing ``;`` followed by ``cat example-project/Project.toml``.

We can also see that there's another file in the ``example-project`` directory
called ``Manifest.toml``...

.. callout:: ``Project.toml`` and ``Manifest.toml``
   
   ``Project.toml`` describes a project on a high level, including 
   package dependencies and compatibilities, metadata such as `authors`,
   `name`, `version` etc. It can be modified by hand. ``Manifest.toml`` 
   is an absolute record of the state of packages in an environment and 
   can be used to create identical Julia environments on different computers.
   It should not be modified by hand.




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
     
