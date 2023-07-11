Potential Gain Add-On
=====

Layout
------------

The overall layout of the Potental Gain Add-On looks like this.

.. jupyter-execute::
    :hide-code:

    import ipyvuetify as v
    
    date_text = v.TextField(label="Start Date", 
                            hint="MM/DD/YYYY format", 
                            persistent_hint=True, 
                            prepend_icon='event', 
                            v_model=sdate.strftime('%m/%d/%Y'))  
    
    date_text2 = v.TextField(label="End Date", 
                             hint="MM/DD/YYYY format", 
                             persistent_hint=True, 
                             prepend_icon='event', 
                             v_model=edate.strftime('%m/%d/%Y'))
    
    # Button and dialog
    dialog = v.Dialog(v_model=False, children=[
        v.Btn(slot="activator", color="primary", children=["Get Dates"])
        ])
    
    line_selector = v.Select(
                label="Select Lines",
                items=[line for line in list_of_line_strings],
                v_model="",
                multiple=True,
            )
    
    parameter_selector = v.Select(
                label="Select Parameter",
                items=['Cheapest Cost/Board Ft','Average Cost/Board Ft','Total Production','Best Case Potential Savings','Average Case Potential Savings'],
                v_model="",
                multiple=True,
            )
    
    user_guide = v.Btn(
                    class_="ma-2",
                    outlined=True,
                    href="https://seeq-cost-throughput-curve-guide.readthedocs.io/en/latest/",
                    children=["User Guide"]
                )
    
    togglesteady = v.Switch(label='Steady State', v_model=True)
    
    results_container = v.Container(fluid=True, children=["Results and visualizations will be displayed here"])
    results_container.children = [output]
    
    app = v.Layout(
        children=[
            v.AppBar(app=True, dark=True, color = '#003057', children=[
                v.ToolbarTitle(children=['Possible Cost Gain XPS Foam Product']),
                v.Spacer(),
                user_guide
            ]),
            v.Container(fluid=True, class_='pt-10', children=[
                v.Row(children=[
                    v.Col(children=[
                        line_selector,parameter_selector,
                        v.Row(children=[
                                v.Col(cols="4", children=[date_text]),
                                v.Col(cols="4", children=[date_text2]),
                                v.Col(cols="2", children=[dialog]),
                                v.Col(cols="2", children=[togglesteady])
                            ])
                            ])
                ]
                     ),
                v.Row(children=[results_container])])
            
        ]
    )

    app

Creating recipes
----------------

To retrieve a list of random ingredients,

.. jupyter-execute::

  name = 'world'
  print('hello ' + name + '!')


you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

.. jupyter-execute::

  name = 'world'
  print('hello ' + name + '!')
