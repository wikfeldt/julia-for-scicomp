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
| Basic arithmetic | - ``2 + 3 * 1.1``                  | - Summing, multiplying          |
|                  | - ``2^3``                          | - Power                         |
|                  | - ``exp(pi*im)``                   | - Complex exponentiation        |
|                  | - ``sin(2*pi)``                    | - Trigonometry                  |
+------------------+------------------------------------+---------------------------------+
| Variables        | - ``A = 3.14``                     | - Scalar, float                 |
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
| 1D arrays        | - ``a = [1, 2, 3, 4]``             | - 4-element Vector{Int64}       |
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
|                  | - ``a[3:end]``                     | - ``end`` is last element       |
+------------------+------------------------------------+---------------------------------+
| Multidimensional | - ``mat = [1 2; 3 4]``             | - 2×2 Matrix{Int64}             |
| arrays           |                                    |                                 |
+------------------+------------------------------------+---------------------------------+
