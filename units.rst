Unit manipulation
=================

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

The `astropy.constants` module contains physical constants relevant for
Astronomy, and these are defined with units attached to them using the
``astropy.units`` framework. If we want to compute the Gravitational force felt by a 100. * u.kg space probe by the Sun, at a distance of 3.2au, we can do::

    >>> from astropy.constants import G

    >>> F = (G * 1. * u.M_sun * 100. * u.kg) / (3.2 * u.au)**2

    >>> F
    <Quantity 6.517421874999999e-10 m3 solMass / (AU2 s2)>

    >>> F.to(u.N)
    <Quantity 0.05792707869188191 N>

The full list of available physical constants is shown HERE (and additions are welcome!).