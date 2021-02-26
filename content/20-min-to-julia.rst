20 minutes to Julia
===================

.. questions::

   - What does the basic syntax of Julia look like?
   - How does Julia handle types?
   - What IDEs and editors work with Julia?

.. objectives::

   - Get familiar with the basics of Julia in 20 minutes.


This section give a compact overview of the basic features
and syntax of Julia.

Running Julia
-------------

After installing Julia, you can run Julia code in various ways:

1. `REPL <https://docs.julialang.org/en/v1/stdlib/REPL/>`_

   A REPL (read-evaluate-print loop) reads input, evaluates
   the expression, prints any output and then loops back.
   Julia's REPL is highly versatile and is useful for exploratory work.
   The Julia REPL has four modes:
   
     - **Julian mode** - default mode where prompt starts with ``julia>``.
       Here you enter Julia expressions and see output.       
     - Type ``?`` to go to **Help mode** where prompt starts with ``help?>``.
       Julia will print help/documentation on anything you enter.
     - Type ``;`` to go to **Shell mode** where prompt starts with
       ``shell>``. You can type any shell commands as you would from terminal.
     - Type ``]`` to go to **Package mode** where prompt starts with
       ``(@v1.5) pkg>`` (if you have Julia version 1.5). Here you can add
       packages with ``add`, update packages with ``update`` etc. To see
       all options type ``?``.
     - To exit any non-Julian mode, hit Escape key.
       
2. `Jupyter <https://jupyter.org/>`_

   Jupyter notebooks are familiar to many Python and R users. WRITEME

3. `Pluto.jl <https://github.com/fonsp/Pluto.jl>`_

   Pluto offers a similar notebook experience to Jupyter, but apart 
   from being *interactive* it's also *reactive* - changing and rerunning
   a code cell automatically updates all cells that depend on it.
   Pluto also doesn't have any hidden workspace state - removing a code
   cell defining a variable makes that variable undefined.
   

4. Juno or VSCode
   

.. callout::   

   You can copy code cells below by pressing the button in the top right
   corner, and paste into the REPL, a notebook or and IDE.


Basic syntax
------------

Variables
^^^^^^^^^

We only need to specify name and value of variables,
Julia figures out the type:

.. code-block:: julia

   A = 3.14               # scalar, float
   B = 100                # scalar, integer
   C = [1, 2, 3]          # array / column-vector (1,2,3)
   D = [1 2 3]            # 1 by 3 array (1,2,3)
   E = [1 2 3]'           # 3 by 1 array (1,2,3)
   F = [1 2; 3 4]         # 2-by-2 matrix
   S = "hello world"      # string
   x = true               # boolean

To see the type of a variable use `typeof`:

.. code-block:: julia

   typeof()

.. code-block:: none

   test output
   
We can 


   
Arrays
^^^^^^

Constructing a few simple matrices:

.. code-block:: julia

   rand(5)                       # random length-5 vector, uniform numbers in [0,1)
   rand(Int, 5)                  # random length-5 vector with integers
   rand(12,4)                    # random 12×4 matrix
   randn(12)                     # Gaussian random numbers (mean 0, std. dev. 1)
   eye(5)                        # 5×5 identity matrix I
   range(0,stop=2*pi,length=10)  # 100 equally spaced points from 0 to 2*pi
   
   
Types
-----

   - booleans, numbers (int, float), strings and chars
   - vectors, matrices
   - tuples, named tuples
   - dictionaries
   - composite types - structs
   - abstract types - e.g. supertype(Float64)
     
     
Loops and conditionals
----------------------

   - for, if-else, while,
   - iterators


Functions
---------

   - named and anonymous functions
   - optional arguments
   - keyword arguments
   - multiple dispatch
   - splatting



Packages
--------


REPL and IDEs
-------------

A REPL (read-evaluate-print loop) reads input, evaluates
the expression, prints any output and then loops back.
Julia's REPL is highly versatile:

.. code-block:: julia

   > ?sum
   

- Pluto.jl
- Weave.jl
- Jupyter  
  


See also
--------

- `Learn X in Y minutes (Where X = Julia) <https://learnxinyminutes.com/docs/julia/>`
- Berhane, Fisseha. (2019) R vs Julia Cheatsheet. Available at:
  https://datascience-enthusiast.com/R/R_Julia_cheat_sheet.html. (Accessed
  December 21, 2019).
- (2019) The Fast Track to Julia. Available at:
  https://juliadocs.github.io/Julia-Cheat-Sheet/. (Accessed December
  21, 2019).
- Gregory, Victoria, Andrij Stachurski, and Natasha Watkins. (2017a)
  Julia Cheatsheet. Available at:
  https://cheatsheets.quantecon.org/julia-cheatsheet.html. (Accessed
  December 21, 2019).
- Gregory, Victoria, Andrij Stachurski, and Natasha Watkins. (2017b)
  MATLAB–Python–Julia Cheatsheet. Available at:
  https://cheatsheets.quantecon.org/. (Accessed December 21, 2019).
- Johnson, Steven G. (2017) Julia & IJulia Cheat-Sheet (for 18.Xxx at
  MIT). Available at:
  http://math.mit.edu/%7Estevenj/Julia-cheatsheet.pdf. (Accessed
  December 21, 2019).
- Bezanson, Jeff, Stefan Karpinski, Viral Shah, and Alan
  Edelman. (2020) The Julia Language. The Julia Project. Available at:
  Https://raw.githubusercontent.com/JuliaLang/docs.julialang.org/assets/julia-1.5.3.pdf. (Accessed
  January 28, 2021).
