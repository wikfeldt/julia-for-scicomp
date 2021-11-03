Quick Reference
===============

This page provides a quick overview of Julia's syntax and tooling.


Running Julia
-------------

We can write Julia code in various ways:

1. `REPL <https://docs.julialang.org/en/v1/stdlib/REPL/>`_
   (read-evaluate-print-loop). Start it by typing ``julia`` (or
   the full path of your Julia executable) on your command line.
   The REPL has four modes:

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
   Jupyter notebooks are familiar to many Python and R users. 

3. `Pluto.jl <https://github.com/fonsp/Pluto.jl>`_

   Pluto offers a similar notebook experience to Jupyter, but in contrast
   to Jupyter
   Pluto understands global references between cells, and
   reactively re-evaluates cells affected by a code change.

4. `Visual Studio Code <https://code.visualstudio.com/>`_ (VSCode)
   - a full-fledged Integrated Development Environment which is
     very useful for larger codebases. Extensions are needed to
     activate Julia inside VSCode, see the `official documentation
     for instructions <https://code.visualstudio.com/docs/languages/julia>`_.
     
5. A text editor like nano, emacs, vim, etc., followed by running your
   code with ``julia filename.jl``. 


Basic syntax
------------

+------------------+------------------------------------+---------------------------------+
| Feature          | Example syntax                     | Result / meaning                |
+==================+====================================+=================================+
| Arithmetic       | - ``2 + 3 * 1.1``                  | - Summing, multiplying          |
|                  | - ``2^3``                          | - Power                         |
|                  | - ``sqrt(9)``                      | - Square root                   |
|                  | - ``40 / 5``                       | - ``8.0`` (Float)               |
|                  | - ``12 % 2``                       | - ``2`` (remainder)             |
|                  | - ``10^19``                        | - Results in integer overflow!  |
|                  | - ``1e19`` or ``big(10)^19``       | - -> solves the problem         |
|                  | - ``exp(pi*im)``                   | - Exponentiation, imaginary nr. |
|                  | - ``sin(2*pi)``                    | - Trigonometry                  |
+------------------+------------------------------------+---------------------------------+
| Types            | - ``A = 3.14``                     | - Scalar, float                 |
|                  | - ``B = 10``                       | - Scalar, integer               |
|                  | - ``C = "hello"``                  | - String                        |
|                  | - ``D = true``                     | - Boolean                       |
|                  | - ``typeof(A)``                    | - Find type                     |
|                  | - ``println("A = $A")``            | - Print using interpolation     |
+------------------+------------------------------------+---------------------------------+
| Special values   | - ``Inf``                          | - Infinity (e.g. ``1 / 0``)     |
|                  | - ``Nan``                          | - Not a number (e.g. ``0 / 0``) |
|                  | - ``nothing``                      | - e.g. for variables w/o value  |
+------------------+------------------------------------+---------------------------------+
| 1D arrays        | - ``t = (1, 2, 3)``                | - Tuple (immutable)             |
|                  | - ``t = (a=2, b=1+2)``             | - Named tuple, access: ``t.a``  |
|                  | - ``d = Dict("A"=>1, "B"=>2)``     | - Dictionary                    |
|                  | - ``a = [1, 2, 3, 4]``             | - 4-element Vector{Int64}       |
|                  | - ``Float64[1,2]``                 | - 2-element Vector{Float64}     |
|                  | - ``[1:5;]``                       | - 5-element Array{Int64,1}      |
|                  | - ``[1:5]``                        | - 1-element vector with a range |
|                  | - ``[range(0,stop=2π,length=5);]`` | - 5-element Vector{Float64}     |
|                  | - ``rand(5)``                      | - random 5-elem vector in [0,1) |
|                  | - ``rand(Int, 5)``                 | - random vector with integers   |
|                  | - ``ones(5)``                      | - 5-elem vector with FP64 ones  |
|                  | - ``zeros(5)``                     | - 5-elem vector with FP64 zeros |
+------------------+------------------------------------+---------------------------------+
| Indexing and     | - ``a[1]``                         | - first element                 |
| slicing          | - ``a[1:3]``                       | - 3-element vector              |
|                  | - ``a[3:end]``                     | - ``end`` is last element       |
|                  | - ``a[1:2:end]``                   | - step size of 2                |
|                  | - ``a[3:end]``                     | - ``end`` is last element       |
|                  | - ``splice!(a,2:3)``               | - Remove items at given indices |
+------------------+------------------------------------+---------------------------------+
| Multidimensional | - ``mat = [1 2; 3 4]``             | - 2×2 Matrix{Int64}             |
| arrays           | - ``zeros(4,4,4,4)``               | - Zero 4×4×4×4 Array{Float64, 4}|
|                  | - ``rand(12,4)``                   | - Random 12×4 Matrix{Float64}   |
+------------------+------------------------------------+---------------------------------+
| Inspecting       | - ``length(a)``                    |                                 |
| array properties | - ``first(a)``                     |                                 |
|                  | - ``last(a)``                      |                                 |
|                  | - ``minimum(a)``                   |                                 |
|                  | - ``maximum(a)``                   |                                 |
|                  | - ``argmin(a)``                    |                                 |
|                  | - ``argmax(a)``                    |                                 |
|                  | - ``size(a)``                      |                                 |
+------------------+------------------------------------+---------------------------------+
| Manipulating     | - ``push!(a, 10)``                 | - Append in-place               |
| arrays           | - ``insert!(a, 1, 42)``            | - Insert in given position      |
|                  | - ``append!(a, [3, 5, 7])``        | - Append another array          |
+------------------+------------------------------------+---------------------------------+


Loops and conditionals
----------------------

For loops iterate over iterables, including types like ``Range``,
``Array``, ``Set`` and ``Dict``.

.. code:: julia

	  for i in [1,2,3,4,5]
	      println("i = $i")
	  end

.. code:: julia

	  for (k, v) in Dict("A" => 1, "B" => 2, "C" => 3)
	      println("$k is $v")
	  end

Conditionals work like in other languages.

.. code:: julia
	  
	  if x > 5
	      println("x > 5")
	  elseif x < 5    # optional elseif
	      println("x < 5")
	  else                    # optional else
	      println("x = 5")
	  end
	  
Functions
---------

A function is an object that maps a tuple of argument values to a return value.

Example of a regular, named function:

.. code:: julia

	  function f(x,y)
	      x + y   # can also use return keyword to return immediately 
	  end

A more compact form:

.. code:: julia

	  f(x,y) = x + y	  

This function can be called by ``f(4,5)``.	  

The expression ``f`` refers to the function object, and can be passed
around like any other value (functions in Julia are `first-class objects`):

.. code:: julia

	  g = f;
	  g(4,5)

Functions can be combined by composition:

.. code::

   f(x) = x^2
   g(x) = sqrt(x)

   f(g(3))   # returns 3.0

An alternative syntax is to use ∘ (typed by ``\circ<tab>``)   

.. code:: julia

	  (f ∘ g)(3)   # returns 3.0 

Most operators (``+``, ``-``, ``*`` etc) are in fact functions, and can be used as such:

.. code:: julia

	  +(1, 2, 3)   # 6

	  # composition:
	  (sqrt ∘ +)(3, 6)  # 3.0 (first summation, then square root)
	  
Keyword arguments can be added after ``;``, which is useful for functions
with many arguments and it can be difficult to remember the correct order:

.. code:: julia
	  
	  function greet_dog(; greeting = "Hi", dog_name = "Fido")  # note the ;
	      println("$greeting $dog_name")
	  end

	  greet_dog(dog_name = "Coco")   # "Hi Coco"


Optional arguments are given default value:

.. code:: julia

	  function date(y, m=1, d=1)
	      month = lpad(m, 2, "0")  # lpad pads from the left
	      day = lpad(d, 2, "0")
	      println("$y-$month-$day")
	  end

	  date(2021)   # "2021-01-01
	  date(2021, 2)   # "2021-02-01
	  date(2021, 2, 3)   # "2021-02-03
	  
Return types can be specified explicitly:

.. code:: julia

   function g(x, y)::Int8
       return x * y
   end

Argument types can also be specified:

.. code:: julia

   function f(x::Float64, y::Float64)
       return x*y
   end
      
As functions in Julia are first-class objects, they can be passed
as arguments to other functions.
`Anonymous functions` are useful for such constructs:

.. code:: julia

   map(x -> x^2 + 2x - 1, [1, 3, -1])  # passes each element of the vector to the anonymous function

   
`Varargs` functions can take an arbitrary number of arguments:

.. code:: julia

	  f(a,b,x...) = a + b + sum(x)

	  f(1,2,3)     # 6
	  f(1,2,3,4)   # 10

"Splatting" is when values contained in an iterable collection
are split into individual arguments of a function call:

.. code:: julia

	  x = (3, 4, 5)

	  f(1,2,x...)    # 15

	  # also possible:
	  x = [1, 2, 3, 4, 5]

	  f(x...)    # 15	  


Julia functions can be piped (chained) together:

.. code:: julia

	  1:10 |> sum |> sqrt    # 7.416198487095663 (first summed, then square root)

	  
	 
