Celestial Coordinates
=====================

Astropy includes a framework to represent celestial coordinates and transform
between them. Astropy 0.2 only includes a few common coordinate systems (ICRS,
FK4, FK5, and Galactic), but future versions will include more built-in
coordinate systems, and users can already define their own systems. In addition,
while the current version only supports transformation of individual scalar
coordinates, arrays will be supported in future.

Coordinate objects are instantiated with a flexible and natural approach that
supports both numeric angle values and (limited) string parsing::

    >>> from astropy import coordinates as coord
    >>> from astropy import units as u
    >>> coord.ICRSCoordinates(ra=10.68458, dec=41.26917, unit=(u.degree, u.degree))
    <ICRSCoordinates RA=10.68458 deg, Dec=41.26917 deg>
    >>> coord.ICRSCoordinates('00h42m44.3s +41d16m9s')
    <ICRSCoordinates RA=10.68458 deg, Dec=41.26917 deg>

The individual components of a coordinate are ``Angle`` objects, and their
values are accessed using special attributes::

    >>> c = coord.ICRSCoordinates(ra=10.68458, dec=41.26917, unit=(u.degree, u.degree))
    >>> c.ra
    <RA 10.68458 deg>
    >>> c.ra.hours
    0.7123053333333333
    >>> c.ra.hms
    (0.0, 42, 44.2992000000001)
    >>> c.dec
    <Dec 41.26917 deg>
    >>> c.dec.radians
    0.7202828960652683

To convert to some other coordinate system, the easiest method is to use
attribute-style access with short names for the built-in systems::

    >>> c.galactic
    <GalacticCoordinates l=121.17422 deg, b=-21.57283 deg>

but explicit transformations via the `transform_to` method are also
available::

    >>> c.transform_to(coord.GalacticCoordinates)
    <GalacticCoordinates l=121.17422 deg, b=-21.57283 deg>

The `Coordinates` subpackage also provides a quick way to get coordinates for
named objects (with an internet connection). All coordinate classes have a
special class method, `from_name()`, that accepts a string and queries `Sesame
<http://cds.u-strasbg.fr/cgi-bin/Sesame>`_ to retrieve coordinates for that
object::

    >>> c_eq = coord.ICRSCoordinates.from_name("M16")
    >>> c_eq
    <ICRSCoordinates RA=274.70000 deg, Dec=-13.80670 deg>

This works for any coordinate class::

    >>> c_gal = coord.GalacticCoordinates.from_name("M42")
    >>> c_gal
    <GalacticCoordinates l=16.95408 deg, b=0.79335 deg>

.. note::

    This is intended to be a convenience, and is very simple. If you
    need precise coordinates for an object you should find the appropriate
    reference for that measurement and input the coordinates manually.
    
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