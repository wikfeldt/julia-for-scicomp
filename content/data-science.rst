Working with data
=================

.. questions::

   - How can I manipulate and wrangle data in Julia?
   - What packages exist?
     
.. objectives::

   - Learn to efficiently use data frames 
   - Learn some good practices around tidy data


Julia is a good language to use for data science problems.
It will perform well, alleviating the need to translate
computationally demanding parts to another language, and its 
ecosystem of libraries for data science and machine learning 
problems is mature and user friendly.

In this episode we will learn how to work with data using 
the DataFrames package and get a flavor for how to set up a 
deep learning workflow using the Flux package.

Download a dataset
------------------

We start by downloading a dataset containing measurements 
of characteristic features of different penguin species.


.. figure:: img/lter_penguins.png
   :align: center

   Artwork by @allison_horst

To obtain the data we simply add the PalmerPenguins package.

.. code-block:: julia

   Pkg.add("PalmerPenguins")
   using PalmerPenguins

.. callout:: Accessing a library of datasets

   The R language (and many of its add-on packages)
   ships with a large number of datasets useful 
   for teaching and statistical software development. These 
   datasets are available in Julia through the 
   `RDatasets <https://github.com/JuliaStats/RDatasets.jl>`_ 
   package:

   .. code-block:: julia

      Pkg.add("RDatasets")
      using RDatasets
      # load a couple of datasets
      iris = dataset("datasets", "iris")
      neuro = dataset("boot", "neuro")

Dataframes
----------

The `DataFrames.jl <https://dataframes.juliadata.org/stable/>`_ 
package is Julia's version of the ``pandas`` library in Python and 
the ``data.frame()`` function in R. We will use it here to 
analyze the penguins dataset, but first we need to install it:

.. code-block:: 

   Pkg.add("DataFrames")
   using DataFrames


.. type-along:: Dataframes

   A dataframe is a 2-dimensional table of rows and columns, much 
   like a Excel spreadsheet. The rows usually represent independent 
   observations, while the columns represent the 
   features (variables) for each observation. Just like in Python and R, 
   the DataFrames.jl package provides functionality for data 
   manipulation and analysis.  
   Here's how you can create a new dataframe:

   .. code-block:: julia

      using DataFrames
      names = ["Ali", "Clara", "Jingfei", "Stefan"]
      age = ["25", "39", "64", "45"]
      df = DataFrame(; name=names, age=age)

   .. code-block:: text

      4×2 DataFrame
       Row │ first_name  age    
           │ String      String 
       ────┼────────────────────
         1 │ Ali         25
         2 │ Clara       39
         3 │ Jingfei     64
         4 │ Stefan      45


We now create a dataframe containing the PalmerPenguins dataset:

.. code-block:: julia

   table = PalmerPenguins.load()
   df = DataFrame(table)

   # the raw data can be loaded by
   #tableraw = PalmerPenguins.load(; raw = true)

   first(df, 5)

.. code-block:: text

   344×7 DataFrame
    Row │ species    island     bill_length_mm  bill_depth_mm  flipper_length_mm  body_mass_g  sex     
        │ String     String     Float64?        Float64?       Int64?             Int64?       String? 
   ─────┼──────────────────────────────────────────────────────────────────────────────────────────────
      1 │ Adelie   Torgersen            39.1           18.7                181         3750  male
      2 │ Adelie   Torgersen            39.5           17.4                186         3800  female
      3 │ Adelie   Torgersen            40.3           18.0                195         3250  female
      4 │ Adelie   Torgersen       missing        missing              missing      missing  missing 
      5 │ Adelie   Torgersen            36.7           19.3                193         3450  female


We can inspect the data using a few basic operations:

.. code-block:: julia

   # slicing
   df[1, 1:3]

   # slicing and column name (can also use "island")
   df[1:20:100, :island]

   # dot syntax (editing will change the dataframe)
   df.species

   # get a copy of a column 
   df[:, [:sex, :body_mass_g]]

   # access column directly without copying (editing will change the dataframe)
   df[!, :bill_length_mm]

   # get size
   size(df), ncol(df), nrow(df)

   # find unique species
   unique(df.species)


Summary statistics can be displayed with the ``describe`` function:

.. code-block:: julia

   describe(df)

.. code-block:: text

   7×7 DataFrame
    Row │ variable           mean     min     median  max        nmissing  eltype                  
        │ Symbol             Union…   Any     Union…  Any        Int64     Type                    
   ─────┼──────────────────────────────────────────────────────────────────────────────────────────
      1 │ species                     Adelie          Gentoo            0  String
      2 │ island                      Biscoe          Torgersen         0  String
      3 │ bill_length_mm     43.9219  32.1    44.45   59.6              2  Union{Missing, Float64}
      4 │ bill_depth_mm      17.1512  13.1    17.3    21.5              2  Union{Missing, Float64}
      5 │ flipper_length_mm  200.915  172     197.0   231               2  Union{Missing, Int64}
      6 │ body_mass_g        4201.75  2700    4050.0  6300              2  Union{Missing, Int64}
      7 │ sex                         female          male             11  Union{Missing, String}

The main features we are interested in for each penguin observation are 
`bill_length_mm`, `bill_depth_mm`, `flipper_length_mm` and `body_mass_g`.
What the first three features mean is illustrated in the picture below.

.. figure:: img/culmen_depth.png
   :align: center

   Artwork by @allison_horst



Let us now look at different ways to visualize this data.

Plotting
--------

Many different plotting libraries exist for Julia and which 
one to use will depend on the specific use case as well as 
personal preference. 

.. callout:: Some plotting packages in Julia
      
   - `Plots.jl <http://docs.juliaplots.org/latest/>`_: high-level 
     API for working with several different plotting back-ends, including `GR`, 
     `Matplotlib.Pyplot`, `Plotly` and `PlotlyJS`
   
      - reliable and simple
      - large JIT precompilation time
   
   - `GadFly.jl <http://gadflyjl.org/stable/>`_: based largely on 
     `ggplot2 for R <https://ggplot2.tidyverse.org/>`_ and the book 
     `The Grammar of Graphics <https://www.cs.uic.edu/~wilkinson/TheGrammarOfGraphics/GOG.html>`_.
   
      - pure Julia, precompiles fast
      - interactive with Javascript integration
      - not the most diverse
   
   - `VegaLite.jl <https://www.queryverse.org/VegaLite.jl/stable/>`_: based on 
     `Vega-Lite <https://vega.github.io/vega-lite/>`_, a grammar of interactive graphics
   
      - like Julia's version of Pythons Seaborn library
      - lacks interactivity
   
   - `Makie.jl <https://makie.juliaplots.org/stable/>`_ data visualization ecosystem with backends 
     `GLMakie.jl` (OpenCL), `CairoMakie.jl` (Cairo) and `WGLMakie.jl` (WebGL)
   
      - pure Julia, high-performance and extendable
      - somewhat less mature
   
We will first create a few graphs using `Plots.jl` and its extension
`StatsPlots.jl` and then 
move on to using `Makie.jl` for visualizing the Penguins dataset.

First we install `Plots.jl` and the `GR` backend:

.. code-block:: julia

   Pkg.add("Plots")
   Pkg.add("GR")


.. type-along:: Starting with the basics

   Here's how a simple line plot works:

   .. code-block:: julia

      using Plots 
      gr()  # set the backend to GR

      x = 1:10; y = rand(10, 2) 
      plot(x, y, title = "Two Lines", label = ["Line 1" "Line 2"], lw = 3) 

   In VSCode, the plot should appear in a new plot pane.  
   We can add labels:

   .. code-block:: julia

      xlabel!("x label")
      ylabel!("y label")

   To add a line to an existing plot, we mutate it with ``plot!``:

   .. code-block:: julia

      z = rand(10)
      plot!(x, z)

   Finally we can save to the plot to a file:

   .. code-block:: julia

      savefig("myplot.png")

   Multiple subplots can be created by:

   .. code-block:: julia

      y = rand(10, 4)

      p1 = plot(x, y) # Make a line plot
      p2 = scatter(x, y) # Make a scatter plot
      p3 = plot(x, y, xlabel = "This one is labelled", lw = 3, title = "Subtitle")
      p4 = histogram(x, y) # Four histograms each with 10 points? Why not!
      plot(p1, p2, p3, p4, layout = (2, 2), legend = false)


Flux.jl
-------

- Flux's core feature is taking gradients of Julia code
- The gradient function takes another Julia function f and a set of
  arguments, and returns the gradient with respect to each argument.


Training a model
^^^^^^^^^^^^^^^^

To train a model we need four things:

- A objective function, that evaluates how well a model is doing given
  some input data.
- The trainable parameters of the model.
- A collection of data points that will be provided to the objective
  function.
- An optimiser that will update the model parameters appropriately.



See also
--------

- `Best Julia Data Manipulation packages combo 2020-09 <https://www.youtube.com/watch?v=q_P2H_ZXVxI>`__

     
