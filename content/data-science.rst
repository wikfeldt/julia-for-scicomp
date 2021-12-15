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

To obtain the data we simply add the PalmerPenguins package.

pkg> add PalmerPenguins
julia> using PalmerPenguins

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


We will need the `DataFrames <https://github.com/JuliaData/DataFrames.jl>`_ 
package:

.. code-block:: 

   Pkg.add("DataFrames")
   using DataFrames


.. callout:: Dataframes

   A dataframe is a 2-dimensional table of rows and columns, much 
   like a Excel spreadsheet. The rows usually represent "samples", 
   i.e. independent observations, while the columns represent the 
   observable features for each sample. Just like in Python and R, 
   the DataFrames.jl package provides functionality for data 
   manipulation and analysis.

julia> table = PalmerPenguins.load()
julia> df = DataFrame(table)

julia> tableraw = PalmerPenguins.load(; raw = true)


.. figure:: img/lter_penguins.png
   :align: center

   Artwork by @allison_horst

	   
.. figure:: img/culmen_depth.png
   :align: center

   Artwork by @allison_horst



Dataframes
----------


Plotting
--------


Plotting with Makie
-------------------


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

     
