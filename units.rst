Unit manipulation
=================

Documentation
-------------

For more information about the features presented below, you can read the
`astropy.units <http://docs.astropy.org/en/v0.2/units/index.html>`_ docs.

Representing units and quantities
----------------------------------

Astropy includes a powerful framework for units that allows users to attach
units to scalars and arrays, and manipulate/combine these, keeping track of
the units.

Since we may want to use a number of units in expressions, it is easiest and
most concise to import the units module with::

    from astropy import units as u

though note that this will conflict with any variable called ``u``.

Units can then be accessed with::

    >>> u.m
    Unit("m")

    >>> u.pc
    Unit("pc")

    >>> u.s
    Unit("s")

    >>> u.kg
    Unit("kg")

We can create composite units:

    >>> u.m / u.kg / u.s**2
    Unit("m / (kg s2)")

The most useful feature about the units is the ability to attach them to
scalars or arrays, creating ``Quantity`` objects::

    >>> 3. * u.m
    <Quantity 3.0 m>

    >>> import numpy as np

    >>> np.array([1.2, 2.2, 1.7]) * u.pc / u.year
    <Quantity [ 1.2  2.2  1.7] pc / (yr)>

Combining and converting units
------------------------------

Quantities can then be combined::

    >>> q1 = 3. * u.m

    >>> q2 = 5. * u.cm / u.s / u.g**2

    >>> q1 * q2
    <Quantity 15.0 cm m / (g2 s)>

and converted to different units::

    >>> (q1 * q2).to(u.m**2 / u.kg**2 / u.s)
    <Quantity 150000.0 m2 / (kg2 s)>

The units and value of a quantity can be accessed separately via the ``value`` and ``unit`` attributes::

    >>> q = 5. * u.pc

    >>> q.value
    5.0

    >>> q.unit
    Unit("pc")

Advanced features
-----------------

The units of a quantity can be decomposed into a set of base units using the
``decompose()`` method. By default, units will be decomposed to S.I.::

    >>> (3. * u.cm * u.pc / u.g / u.year**2).decompose()
    <Quantity 929.5706802193289 m2 / (kg s2)>

To decompose into c.g.s. units, one can do::

    >>> (3. * u.cm * u.pc / u.g / u.year**2).decompose(u.cgs.bases)
    <Quantity 9295.70680219329 cm2 / (g s2)>

Using physical constants
------------------------

The `astropy.constants
<http://docs.astropy.org/en/v0.2/constants/index.html>`_ module contains
physical constants relevant for Astronomy, and these are defined with units
attached to them using the ``astropy.units`` framework. If we want to compute
the Gravitational force felt by a 100. * u.kg space probe by the Sun, at a
distance of 3.2au, we can do::

    >>> from astropy.constants import G

    >>> F = (G * 1. * u.M_sun * 100. * u.kg) / (3.2 * u.au)**2

    >>> F
    <Quantity 6.517421874999999e-10 m3 solMass / (AU2 s2)>

    >>> F.to(u.N)
    <Quantity 0.05792707869188191 N>

The full list of available physical constants is shown `here <http://docs.astropy.org/en/v0.2/constants/index.html#module-astropy.constants>`_ (and additions are welcome!).

Practical Exercises
-------------------

.. admonition::  Level 1

    What is 1 barn megaparsecs in teaspoons?

.. raw:: html

   <p class="flip1">Click to Show/Hide Solution</p> <div class="panel1">

::

    >>> (1. * u.barn * u.Mpc).to(u.tsp)
    <Quantity 0.626035029893 tsp>

.. raw:: html

   </div>

.. admonition::  Level 2

    What is 3 nm^2 Mpc / m^3 in dimensionless units?

.. raw:: html

   <p class="flip2">Click to Show/Hide Solution</p> <div class="panel2">

::

    >>> (3. * u.nm**2 * u.Mpc / u.m**3).decompose()
    <Quantity 92570.327444 >

or to just get the numerical value::

    >>> (3. * u.nm**2 * u.Mpc / u.m**3).decompose().value
    92570.327444015755

.. raw:: html

   </div>

.. admonition::  Level 3

    Try and convert 3 microns to eV using the units framework. You will need
    to look through the documentation for `astropy.units <http://docs.astropy.org/en/v0.2/units/index.html>`_ to see how this can be made to work.

.. raw:: html

   <p class="flip3">Click to Show/Hide Solution</p> <div class="panel3">

::

    >>> (3 * u.micron).to(u.eV)
    ...
    UnitsException: 'micron' (length) and 'eV' (energy) are not convertible

    >>> (3 * u.micron).to(u.eV, equivalencies=u.spectral())
    <Quantity 0.413280643067 eV>

.. raw:: html

   </div>
