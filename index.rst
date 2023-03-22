:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

Checks the performance of the TMA under 3.5 degree random offsets tracking for 32 seconds (and back to original position) in the full range of azimuth and elevation (another az-el grid).  Checks jitter, slew and settle against encoders in the EFD. Requirements that must be met are documented in LTS 103. We require slew and settle time to be less than 4s for zenith angles greater than 30 degrees and the mount jitter to be less than 0.01 arcsec in an image. 


Methodology
===========

On March 9, 2023, we used the following test strategy to check the stability of the TMA under slews.

1. Take 3 images in one location.
2. Move 3.5 degrees in a random direction and take 3 images there.
3. Return to location (1) and take three more images.
4. Repeat steps 2 and 3 four more times.
5. Move to new location and repeat steps 1 – 4.

An example set of image locations for is shown in Fig. :ref:`1<fig-ellipse>`.

.. figure:: /_static/ellipse.png
    :name: fig-ellipse

    A sample set of points with the center position and 5 points offset by 3.5 degrees in a random direction.

Analysis
========

Slew and Settle Tests
---------------------

We evaluate the slew and settle performance.  For the first correctly computed offset test we performed on March 9, we seee azimuth and elevation changes are:

.. figure:: /_static/Az_1.png
    :name: fig-az-1

    Azimuth positions for first 3.5 degree offset test on March 9, 2023.

.. figure:: /_static/El_1.png
    :name: fig-el-1

    Elevation positions for first 3.5 degree offset test on March 9, 2023.

We then isolate the slew times based on when the mount encoder data shows that azimuth or elevation are changing at a sufficiently fast(?) rate. Here is an example plot for the above test:

.. figure:: /_static/slew_pos_1.png
    :name: fig-slew-pos

    Slew times for first 3.5 degree offset test on March 9, 2023.

We then plot the slew times for all slews

.. figure:: /_static/Slew_all_1.png
    :name: fig-slew-all-1

    Slew times for first 3.5 degree offset test on March 9, 2023.

and the slew time for slews that were between 3 and 4 degrees.

.. figure:: /_static/Slew_3_5_1.png
    :name: fig-slew-3.5-1

    Slew times for 3.5 degree slews for the first 3.5 degree offset test on March 9, 2023.


We repeat the same test for another round of slews on March 9:

.. figure:: /_static/az_2.png
    :name: fig-az-2

    Azimuth positions for second 3.5 degree offset test on March 9, 2023.

.. figure:: /_static/el_2.png
    :name: fig-el-2

    Elevation positions for second 3.5 degree offset test on March 9, 2023.

.. figure:: /_static/slew_all_2.png
    :name: fig-slew-all-2

    Slew times for second 3.5 degree offset test on March 9, 2023.

.. figure:: /_static/Slew_3_5_2.png
    :name: fig-slew-3.5-2

    Slew times for 3.5 degree slews for the second 3.5 degree offset test on March 9, 2023.

And additionally we repeat this for tests on March 15, 2023:

.. figure:: /_static/az_3.png
    :name: fig-az-3

    Azimuth positions for a 3.5 degree offset test on March 15, 2023.

.. figure:: /_static/el_3.png
    :name: fig-el-3

    Elevation positions for a 3.5 degree offset test on March 15, 2023.

.. figure:: /_static/Slew_all_3.png
    :name: fig-slew-all-3

    Slew times for a 3.5 degree offset test on March 15, 2023.

.. figure:: /_static/Slew_3_5_3.png
    :name: fig-slew-3.5-3

    Slew times for 3.5 degree slews for the second 3.5 degree offset test on March 15, 2023.


We see that for the 3.5 degree slews, the slew and settle time is always less than 4 seconds.

Jitter Tests
------------

For the jitter tests, we look at how much jitter there is during the StarTracker exposures. Specifically, we fit the azimuth and elevation mount encoder data to a fourth order polynomial and then compute the rms of the residuals. A sample plot is shown here:

.. figure:: /_static/jitter_sample.png
    :name: fig-jitter-sample

    Sample jitter plot for one exposure.


We see that there are outliers due to electrical spikes. We remove all points that are 10 :math:`\sigma` outliers and then compute the rms jitter based on that. We then plot the histograms of jitter for all images below.

For the different offset tests, we see:

.. figure:: /_static/jitter_1.png
    :name: fig-jitter-1

    Histogram of jitter for the first offset test on March 9, 2023.

.. figure:: /_static/jitter_2.png
    :name: fig-jitter-2

    Histogram of jitter for the second offset test on March 9, 2023.

.. figure:: /_static/jitter_3.png
    :name: fig-jitter-3

    Histogram of jitter for the offset test on March 15, 2023.

We see that with one exception (which is clearly an outlier), all jitter is less than 0.01 arcsec, which is within the requirements.

StarTracker Jitter Tests
^^^^^^^^^^^^^^^^^^^^^^^^

We also analyze 1000 images of a double star taken with the fast StarTracker camera at 100 Hz over the course of 10 seconds on March 17, 2023. This camera has a plate scale of 0.62 arcsec/pixel. In the image below we can see a drift in the y centroid over time, which we expect from the pointing model. The rms jitter in x is ~0.2 arcsec, which could be due to atmospheric turbulence.

.. figure:: /_static/startracker_centroid.png
    :name: fig-star-centroid

    Plots of flux and centroid of one of the stars taken with the StarTracker fast camera at 100 Hz for 10 seconds. 

We also FFT the centroid positions to look for 

.. figure:: /_static/startracker_fft.png
    :name: fig-fft-star

    Absolute value of the FFT of the x and y centroids for both sources in the image.

.. figure:: /_static/startracker_fft_zoom.png
    :name: fig-fft-zoom

    Zoom in of the absolute value of the FFT of the x and y centroids for both sources in the image.

There also seems to be some periodic jitter with frequency of about 1 Hz. This could be due to mount motion and needs to be correlated with the accelerometer data.

Summary
=======

Slews of 3.5 degrees are always completed in less than 4 seconds, which is within requirements.

The jitter is within requirements when we check the mount encoder data and remove outlier datapoints. It is still unclear why these outliers are being read into the EFD.

There may be a ~1 Hz oscillation visible in the fast StarTracker data. We should look at more data and correlate with accelerometer readings to properly do the comparison.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
