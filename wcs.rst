WCS Transformations
===================

.. note:: If you are already familiar with PyWCS, `astropy.wcs` is in fact the
          same code as the latest version of PyWCS, and you can adapt old
          scripts that use PyWCS to use Astropy by simply doing::

              from astropy import wcs as pywcs

          However, for new scripts, we recommend the following import::

              from astropy.wcs import WCS

          since most of the user-level functionality is contained within the `WCS` class.

Representing WCS transformations
--------------------------------

The World Coordinate System standard is often used in FITS files in order to
describe the conversion from pixel to world (e.g. equatorial, galactic, etc.)
coordinates. Given a FITS file with WCS information, such as ``MSX_E.fits``,
we can create an object to represent the WCS transformation either by directly
supplying the filename::

    >>> from astropy.wcs import WCS
    >>> w = WCS('MSX_E.fits')

or the header of the FITS file::

    >>> from astropy.io import fits
    >>> from astropy.wcs import WCS
    >>> header = fits.getheader('MSX_E.fits')
    >>> w = WCS(header)

Pixel to World and World to Pixel transformations
-------------------------------------------------

Once the WCS object has been created, you can use the following methods to
convert pixel to world coordinates::

    >>> wx, wy = w.wcs_pix2world(22., 32., 1)
    >>> print wx, wy
    0.462713344530996 -0.445656677451558

This converts the pixel coordinates (22, 32) to the native world coordinate
system of the transformation. Note the third argument, set to ``1``, which
indicates whether the pixel coordinates should be treated as starting from (1,
1) (as FITS files do) or from (0, 0). Converting from world to pixel
coordinates is similar::

    >>> px, py = w.wcs_world2pix(0., 0., 1)
    >>> print px, py
    299.628 299.394

Working with arrays
-------------------

If many coordinates need to be transformed, then it is possible to use Numpy arrays::

    >>> import numpy as np
    >>> px = np.arange(10)
    >>> py = np.repeat(10., 10)
    >>> wx, wy = w.wcs_pix2world(px, py, 1)
    >>> print wx
    [ 0.49938001  0.49771335  0.49604668  0.49438001  0.49271335  0.49104668
      0.48938001  0.48771335  0.48604668  0.48438001]
    >>> print wy
    [-0.48232335 -0.48232335 -0.48232335 -0.48232335 -0.48232335 -0.48232335
     -0.48232335 -0.48232335 -0.48232335 -0.48232335]

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

