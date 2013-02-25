Tabular data
============

Astropy includes a class for representing arbitrary tabular data in
``astropy.table``, called ``Table``. This class can be imported with::

    from astropy.table import Table
    
You may need to also import the ``Column`` class, depending on how you are
definining your table (see below)::

    from astropy.table import Table, Column


Constructing and Manipulating tables
------------------------------------

There are a number of ways of constructing tables. One simple way is to start
from existing lists or arrays::

    >>> from astropy.table import Table
    >>> a = [1, 4, 5]
    >>> b = [2.0, 5.0, 8.2]
    >>> c = ['x', 'y', 'z']
    >>> t = Table([a, b, c], names=('a', 'b', 'c'))

There are a few ways to examine the table.  You can get detailed information
about the table values and column definitions as follows::

  >>> t
  <Table rows=3 names=('a','b','c')>
  array([(1, 2.0, 'x'), (4, 5.0, 'y'), (5, 8.2, 'z')],
        dtype=[('a', '<i8'), ('b', '<f8'), ('c', '|S1')])

If you print the table (either from the noteboook or in a text console
session) then a formatted version appears::

  >>> print t
    a   b   c
  --- --- ---
    1 2.0   x
    4 5.0   y
    5 8.2   z

Now examine some high-level information about the table::

  >>> t.colnames
  ['a', 'b', 'c']

  >>> len(t)
  3

Access the data by column or row using the same syntax as for Numpy structured
arrays::

    >>> t['a']       # Column 'a'
    <Column name='a' units=None format=None description=None>
    array([1, 4, 5])

    >>> t['a'][1]    # Row 1 of column 'a'
    4

    >>> t[1]         # Row obj for with row 1 values
    <Row 1 of table
      values=(4, 5.0, 'y')
      dtype=[('a', '<i8'), ('b', '<f8'), ('c', '|S1')]>

    >>> t[1]['a']    # Column 'a' of row 1
    4

One can retrieve a subset of a table by rows (using a slice) or columns (using
column names), where the subset is returned as a new table::

    >>> print t[0:2]      # Table object with rows 0 and 1
     a   b   c
    --- --- ---
      1 2.0   x
      4 5.0   y

    >>> t['a', 'c']  # Table with cols 'a', 'c'
     a   c
    --- ---
      1   x
      4   y
      5   z

Modifying table values in place is flexible and works as one would expect::

    >>> t['a'] = [-1, -2, -3]       # Set all column values
    >>> t['a'][2] = 30              # Set row 2 of column 'a'
    >>> t[1] = (8, 9.0, "W")        # Set all row values
    >>> t[1]['b'] = -9              # Set column 'b' of row 1
    >>> t[0:2]['b'] = 100.0         # Set column 'c' of rows 0 and 1
    >>> print t
     a    b    c
    --- ----- ---
     -1 100.0   x
      8 100.0   W
     30   8.2   z

Add, remove, and rename columns with the following::

    >>> t.add_column(Column(data=[1, 2, 3], name='d')))
    >>> t.remove_column('c')
    >>> t.rename_column('a', 'A')
    >>> t.colnames
    ['A', 'b', 'd']

Adding a new row of data to the table is as follows::

    >>> t.add_row([-8, -9, 10])
    >>> len(t)
    4

Lastly, one can create a table with support for missing values, for example by setting
``masked=True``::

    >>> t = Table([a, b, c], names=('a', 'b', 'c'), masked=True)
    >>> t['a'].mask = [True, True, False]
    >>> t
    <Table rows=3 names=('a','b','c')>
    masked_array(data = [(--, 2.0, 'x') (--, 5.0, 'y') (5, 8.2, 'z')],
                 mask = [(True, False, False) (True, False, False) (False, False, False)],
           fill_value = (999999, 1e+20, 'N'),
                dtype = [('a', '<i8'), ('b', '<f8'), ('c', '|S1')])

    >>> print t
     a   b   c
    --- --- ---
     -- 2.0   x
     -- 5.0   y
      5 8.2   z

Finally, every table can have meta-data attached to it via the ``meta``
attribute, which can be used like a Python dictionary::

    >>> t.meta['creator'] = 'me'

Reading and writing tables
--------------------------

``Table`` objects include ``read`` and ``write`` methods that can be used to
easily read and write the tables to different formats.

TODO

Practical Exercises
-------------------

.. admonition::  Level 1

    Question here

.. raw:: html

   <p class="flip1">Click to Show/Hide Solution</p> <div class="panel1">

Solution

.. raw:: html

   </div>
   
.. admonition::  Level 2

    Question here

.. raw:: html

   <p class="flip2">Click to Show/Hide Solution</p> <div class="panel2">

Solution

.. raw:: html

   </div>
   
.. admonition::  Level 3

    Question here

.. raw:: html

   <p class="flip3">Click to Show/Hide Solution</p> <div class="panel3">

Solution

.. raw:: html

   </div>
