Cost Throughput Curve
=====

.. jupyter-execute::
    :hide-code:

    import ipyvuetify as v

    my_select = v.Select(
        label='Fruits',
        items=['Apple', 'Pear', 'Cherry'])
    my_select

.. _installation:

Installation
------------

To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

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

