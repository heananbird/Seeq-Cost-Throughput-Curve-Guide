Cost Curve User Guide Documentation
========================

This documentation outlines user guide to use the Cost Throughput Curves and Potential Gain add-ons

Cost Throughput Curves
----------------------

The Cost Throughput Curve addon user guide can be found in :doc:`Cost Throughput Curve <cost>`. This addon uses the calculated metrics to provide a graphic representation about the current and past performance when compared against their cost and throughput.

.. jupyter-execute::
    :hide-code:

    import plotly.express as px
    df = px.data.iris()
    replacement_dict = {'setosa': 'Line 1', 'versicolor': 'Line 2', 'virginica': 'Line 3'}
    df['species'] = df['species'].replace(replacement_dict)
    df = df.rename(columns={'sepal_width':'Variable 1'})
    df = df.rename(columns={'sepal_length':'Variable 2'})
    df = df.rename(columns={'petal_length':'Variable 3'})
    df = df.rename(columns={'species':'Line'})
    df= df.rename(columns={'petal_width':'Production Variable'})
    
    fig = px.scatter(df, x="Variable 1", y="Variable 2", color="Line",
                    size='Variable 3', hover_data=['Production Variable'])
    fig.show()

.. note::

   The Jupyter Notebook for this add on can be found here https://owenscorning.seeq.site/data-lab/04F36E78-6B4E-43A5-A39F-65268550842D/notebooks/Active_Development/Adjust%20BA%20For%20All%20Three%20Possibilities.ipynb

Potential Gain
--------------

The Potential Gain addon user guide can be found in :doc:`Potential Gain <potential>`. This add-on outlines potential improvement of products for performing at the average or **"best in class"** performance.

.. jupyter-execute::
    :hide-code:

    from ipyaggrid import Grid

    grid_options = {
    'columnDefs' : [
        {'headerName': 'Variable 1', 'field': 'Variable 1', 'sortable': True},
        {'headerName': 'Variable 2', 'field': 'Variable 2', 'sortable': True},
        {'headerName': 'Variable 3', 'field': 'Variable 4', 'sortable': True},
        {'headerName': 'Line', 'field': 'Line', 'sortable': True},
        {'headerName': 'Production Variable', 'field': 'Production Variable', 'sortable': True}
    ],
    'enableSorting': True,
    'enableFilter': True,
    'enableColResize': True, 
    'enableRangeSelection': True
}

    grid = Grid(grid_data=df, grid_options=grid_options)

    grid

.. note::

   The Jupyter Notebook for this add on can be found here https://owenscorning.seeq.site/data-lab/04F36E78-6B4E-43A5-A39F-65268550842D/notebooks/Active_Development/Table%20View%20Add%20On.ipynb

Contents
--------

.. toctree::

   cost
   potential
