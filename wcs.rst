WCS Transformations
===================

.. note:: For users previously familiar with PyWCS, `astropy.wcs` is in fact the same code as the latest version of PyWCS, and you can adapt old scripts that use PyWCS to use Astropy by simply doing::

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

or from the header of the FITS file::

    >>> from astropy.io import fits

    >>> header = fits.getheader('MSX_E.fits')

    >>> from astropy.wcs import WCS

    >>> w = WCS(header)

Pixel to World and World to Pixel transformations
-------------------------------------------------

Once the WCS object has been created, one can use the following methods to convert pixel to world coordinates::

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



