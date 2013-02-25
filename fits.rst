Handling FITS files
===================

.. note:: If you are already familiar with PyFITS, `astropy.io.fits` is in
          fact the same code as the latest version of PyFITS, and you can
          adapt old scripts that use PyFITS to use Astropy by simply doing::

              from astropy.io import fits as pyfits

          However, for new scripts, we recommend the following import::

              from astropy.io import fits

Reading FITS files and accessing data
-------------------------------------

Opening a FITS file is relatively straightforward::

    >>> from astropy.io import fits
    >>> hdulist = fits.open('MSX_E.fits')

The returned object, ``hdulist``, behaves like a Python list, and each element
maps to a Header-Data Unit (HDU) in the FITS file. You can view more
information about the FITS file with:

    >>> hdulist.info()
    Filename: MSX_E.fits
    No.    Name         Type      Cards   Dimensions   Format
    0    PRIMARY     PrimaryHDU      23   (599, 599)   float64

As we can see, this file only contains one HDU. To access the primary HDU (the
most common scenario), you can then do::

    >>> hdu = hdulist[0]

The ``hdu`` object then has two important attributes: ``data``, which behaves
like a Numpy array, can be used to access the data, and ``header``, which
behaves like a dictionary, can be used to access the header information::

    >>> hdu.data.shape
    (599, 599)

    >>> hdu.data.mean()
    1.094245431961814e-05

    >>> hdu.header
    SIMPLE  =                    T
    BITPIX  =                  -64
    NAXIS   =                    2
    NAXIS1  =                  599
    NAXIS2  =                  599
    EXTEND  =                    T / FITS dataset may contain extensions
    COMMENT   FITS (Flexible Image Transport System) format is defined in 'Astronomy
    COMMENT   and Astrophysics', volume 376, page 359; bibcode: 2001A&A...376..359H
    CRPIX1  =              299.628
    CRVAL1  =          0.000000000
    CDELT1  =      -0.001666666707
    CTYPE1  = 'GLON-CAR'
    CRPIX2  =              299.394
    CRVAL2  =          0.000000000
    CDELT2  =       0.001666666707
    CTYPE2  = 'GLAT-CAR'
    CROTA2  =          0.000000000
    LONPOLE =          0.000000000
    WAVELENG=          2.13400E-05
    BUNIT   = 'W/m^2-sr'
    TELESCOP= 'MSX     '
    INSTRUME= 'SPIRITIII'
    ORIGIN  = 'AFRL-VSBC'

    >>> hdu.header['TELESCOP']
    'MSX'

Modifying data or header information in a FITS file object is easy::

    >>> hdu.header['TELESCOP'] = "Midcourse Space eXperiment"
    >>> hdu.header['SIGMA'] = 18.  # adds a new keyword
    >>> hdu.data = 2. * hdu.data - 1

Note that this does not change the original FITS file, simply the FITS file
object in memory. You can write the FITS file object to a file with::

    >>> hdu.writeto('scaled_1.fits')

if you want to simply write out this HDU to a file, or::

    >>> hdulist.writeto('scaled_2.fits')

if you want to write out all of the original HDUs, including the modified one,
to a file.

Creating a FITS file from scratch
---------------------------------

If you want to create a FITS file from scratch, you need to start off by creating an HDU object::

    >>> hdu = fits.PrimaryHDU()

and you can then populate the data and header attributes with whatever information you like::

    >>> import numpy as np
    >>> hdu.data = np.random.random((128,128))

Note that setting the data automatically populates the header with basic information:

    >>> hdu.header
    SIMPLE  =                    T / conforms to FITS standard
    BITPIX  =                  -64 / array data type
    NAXIS   =                    2 / number of array dimensions
    NAXIS1  =                  128
    NAXIS2  =                  128
    EXTEND  =                    T

and you should never have to set header keywords such as ``NAXIS``, ``NAXIS1``, and so on manually. We can then set additional header keywords::

    >>> hdu.header['telescop'] = 'Python Observatory'

and we can then write out the FITS file to disk::

    >>> hdu.writeto('random_array.fits')

If the file already exists, you can overwrite it with::

    >>> hdu.writeto('random_array.fits', clobber=True)

Convenience functions
---------------------

In cases where you just want to access the data or header in a specific HDU,
you can use the following convenience functions::

    >>> data = fits.getdata('MSX_E.fits')
    >>> header = fits.getheader('MSX_E.fits')

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