Potential Gain Add-On
=====

Layout - Update
******

The overall layout of the Potental Gain Add-On looks like this. Updated?

.. jupyter-execute::
    :hide-code:

    import ipyvuetify as v
    
    date_text = v.TextField(label="Start Date", 
                            hint="MM/DD/YYYY format", 
                            persistent_hint=True, 
                            prepend_icon='event', 
                            v_model='03/02/2022')
    
    date_text2 = v.TextField(label="End Date", 
                             hint="MM/DD/YYYY format", 
                             persistent_hint=True, 
                             prepend_icon='event', 
                             v_model='04/07/2023')
    
    # Button and dialog
    dialog = v.Dialog(v_model=False, children=[
        v.Btn(slot="activator", color="primary", children=["Get Dates"])
        ])
    
    line_selector = v.Select(
                label="Select Lines",
                items=['Line 1', 'Line 2', 'Line 3', 'Line 4'],
                v_model="",
                multiple=True,
            )
    
    parameter_selector = v.Select(
                label="Select Parameter",
                items=['Fast','Slow','Quick','Top','Bottom'],
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
    
    app = v.Layout(
        children=[
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
                    ])
                ])
            ])

    app

-----

Line Selection
--------------

To select data from a group of lines, click "Select Lines" and pick the one or multiple lines of imterest.

.. jupyter-execute::
    :hide-code:

    line_selector = v.Select(
                label="Select Lines",
                items=['Line 1', 'Line 2', 'Line 3', 'Line 4'],
                v_model="",
                multiple=True,
            )

    app = v.Layout(children=[line_selector])

    app

-----

Parameter Selector
-------------------

To select a single parameter metric or multiple, click "Select Parameters" and pick one or multiple of interest.

.. jupyter-execute::
    :hide-code:

    parameter_selector = v.Select(
            label="Select Parameter",
            items=['Fast','Slow','Quick','Top','Bottom'],
            v_model="",
            multiple=True,
        )
    app = v.Layout(children=[parameter_selector])

    app

.. note::

    Data table will now appear, as you adjust the values in Parameter Selector and Line Selection the table will auto-update.

-----

Date Selection
--------------

Date Selection is split into two parts:

# Start/End Date: Where dates of interest in MM/DD/YYYY Format are placed

.. jupyter-execute::
    :hide-code:

    date_text = v.TextField(label="Start Date",
                            hint="MM/DD/YYYY format",
                            persistent_hint=True,
                            prepend_icon='event',
                            v_model='03/02/2022')

    date_text2 = v.TextField(label="End Date",
                             hint="MM/DD/YYYY format",
                             persistent_hint=True,
                             prepend_icon='event',
                             v_model='04/07/2023')

    app = v.Layout(children=[
                v.Row(children=[
                    v.Col(cols="4", children=[date_text]),
                    v.Col(cols="4", children=[date_text2])
                    ])
                            ]
                    )

    app

# Get Dates Button: When clicked new data is drawn for stored data and tables are updated 

.. jupyter-execute::
    :hide-code:

    dialog = v.Dialog(v_model=False, children=[
        v.Btn(slot="activator", color="primary", children=["Get Dates"])
        ])

    app = v.Layout(children=[dialog])

    app

-----

State Selector
-------------------

Data is split into stead state processes (greater than 4 hours) and transient state process (less than 4 hours). Using this toggle the two groups of data can be transitioned back and forth.

.. jupyter-execute::
    :hide-code:

    togglesteady = v.Switch(label='Steady State', v_model=True)

    app = v.Layout(children=[togglesteady])

    app


