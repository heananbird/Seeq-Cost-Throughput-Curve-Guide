Cost Throughput Curve Add On
============================

Layout
******

The overall layout of the Potental Gain Add-On looks like this.

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
    
    grade_selector = v.Select(
            label="Select Grade",
            items= ['Grade 1', 'Grade 2', 'Grade 3', 'Grade 4'],
            v_model="",
            multiple=True,
        )

    thickness_selector = v.Select(
                label="Select Thickness",
                items= ['Thickness 1', 'Thickness 2', 'Thickness 3', 'Thickness 4'],
                v_model="",
                multiple=True)

    x_axis = v.Select(
                label='X Axis',
                items= ['Variable 1','Variable 2', 'Variable 3'],
                v_model='Variable 1',
                multiple=False)

    y_axis = v.Select(
                label='Y Axis',
                items= ['Variable 1','Variable 2', 'Variable 3'],
                v_model='Variable 2',
                multiple=False)

    z_axis = v.Select(
                label='Z Axis',
                items= ['Variable 1','Variable 2', 'Variable 3'],
                v_model='Variable 3',
                multiple=False)
    
    toggle3D = v.Switch(label='3D Chart', v_model=False)
    
    togglesteady = v.Switch(label='Steady State', v_model=True)
    
    app = v.Layout(children=[
        v.Container(fluid=True, class_='pt-10', children=[
            v.Row(children=[
                v.Col(children=[
                    v.Row(children=[
                        v.Col(cols="4", children=[line_selector]),
                        v.Col(cols="4", children=[grade_selector]),
                        v.Col(cols="4", children=[thickness_selector])
                    ]),
                    
                    v.Row(children=[
                        v.Col(cols="4", children=[x_axis]),
                        v.Col(cols="4", children=[y_axis]),
                        v.Col(cols="4", children=[z_axis])
                    ]),
                    v.Row(children=[
                        v.Col(cols="2", children=[toggle3D]),
                        v.Col(cols="3", children=[date_text]),
                        v.Col(cols="3", children=[date_text2]),
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

Grade And Thickness Selection
-----------------------------

To Filter the data by thickness or grade, a specific or multiple thicknesses or grades can be selected. To see all data for a thickness selection, simply leave the grade selection blank and all grades will be selected. To see all data for a grade selection, simply leave the grade selection blank and all grades will be selected.

.. jupyter-execute::
    :hide-code:

    grade_selector = v.Select(
            label="Select Grade",
            items= ['Grade 1', 'Grade 2', 'Grade 3', 'Grade 4'],
            v_model="",
            multiple=True,
        )

    thickness_selector = v.Select(
                label="Select Thickness",
                items= ['Thickness 1', 'Thickness 2', 'Thickness 3', 'Thickness 4'],
                v_model="",
                multiple=True,
            )
    app = v.Layout(children=[grade_selector, thickness_selector])

    app

-----

Axis Selection
--------------

There are three axis on which to display data, upon loading the add-on the default axis for the Cost Throughput Curves will be displayed. To adjust or change the variables of axis the dropdown for any axis can be selected and modified.

.. jupyter-execute::
    :hide-code:

    x_axis = v.Select(
        label='X Axis',
        items= ['Variable 1','Variable 2', 'Variable 3'],
        v_model='Variable 1',
        multiple=False)

    y_axis = v.Select(
        label='Y Axis',
        items= ['Variable 1','Variable 2', 'Variable 3'],
        v_model='Variable 2',
        multiple=False)

    z_axis = v.Select(
        label='Z Axis',
        items= ['Variable 1','Variable 2', 'Variable 3'],
        v_model='Variable 3',
        multiple=False)

    app = v.Layout(children=[x_axis, y_axis, z_axis])

    app

**To view data in three axis the 3D Chart toggle can be activated.**

.. jupyter-execute::
    :hide-code:

    toggle3D = v.Switch(label='3D Chart', v_model=False)

    app = v.Layout(children=[toggle3D])

    app

..note:

    It can be difficult to understand data shown in 3D when many lines, thickness, and grades are present. It is reccomened to narrow the search field before applying a dimnesional increase.

-----

Date Selection
--------------

Date Selection is split into two parts:

-Start/End Date: Where dates of interest in MM/DD/YYYY Format are placed

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

-Get Dates Button: When clicked new data is drawn for stored data and tables are updated 

.. jupyter-execute::
    :hide-code:

    dialog = v.Dialog(v_model=False, children=[
        v.Btn(slot="activator", color="primary", children=["Get Dates"])
        ])

    app = v.Layout(children=[dialog])

    app

-----

State Selector
--------------

Data is split into stead state processes (greater than 4 hours) and transient state process (less than 4 hours). Using this toggle the two groups of data can be transitioned back and forth.

.. jupyter-execute::
    :hide-code:

    togglesteady = v.Switch(label='Steady State', v_model=True)

    app = v.Layout(children=[togglesteady])

    app

-----

Features
********

-----
Excel Download
--------------

In the right hand corner next to the user guide is a hamburger menu. When this menu is selected a dropdown will display where the Input Values can be updated, updating these values will allow for a Excel file to be downloaded with the production variables data.

.. jupyter-execute::
    :hide-code:

    metric_guide = v.Btn(
                class_="ma-2",
                outlined=True,
                href="",
                target="_blank",
                children=["Calculation Guide PDF"]
            )

    user_guide = v.Btn(
                class_="ma-2",
                outlined=True,
                href="https://seeq-cost-throughput-curve-guide.readthedocs.io/en/latest/",
                target="_blank",
                children=["User Guide"]
            )

    Input_1 = v.TextField(label='Input 1', hint='hint location', persistent_hint=True, v_model='test')
    Input_2 = v.TextField(label='Input 2', hint='hint location', persistent_hint=True, v_model='test')
    Input_3 = v.TextField(label='Input 3', hint='hint location', persistent_hint=True, v_model='test')

    excel_button = v.Btn(children=['Generate'])

    # Hamburger menu button
    hamburger_button = v.AppBarNavIcon(v_on='menuData.on')

    menu_items = [
        v.Col(children=[
                Input_1,
                Input_2,
                Input_3,
                v.Row(children=[v.Spacer(),excel_button,v.Spacer()])
        ])
    ]

    hamburger_menu = v.Menu(offset_y=True, close_on_content_click=False, v_slots=[{
        'name': 'activator',
        'variable': 'menuData',
        'children': hamburger_button,
    }], children=[
        v.List(children=menu_items)
    ])
    
    app = v.Layout(
    children=[v.Row(children=[
            v.ToolbarTitle(children=['Title']),
            hamburger_menu,
            metric_guide,
            user_guide
        ])])

    app

..note:

    Loading times & Generating can be long depending on the time length of data being pulled and updated.

-----
Advanced Line Selection
-------------------

If you click the lines in the legend (right hand side) of the plot. Specfic lines can be selected, unselected, or focused by single or double clicking.

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
