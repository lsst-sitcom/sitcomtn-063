:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

Checks the performance of the TMA under 3.5 degree random offsets in the full range of azimuth and elevation.  Checks jitter, slew and settle against encoders in the EFD and accelerometer data. Requirements that must be met are documented in LTS 103. We require slew and settle time to be less than 4s for zenith angles greater than 30 degrees and the mount jitter to be less than 0.01 arcsec in a 15 s image. 

We find that 4.2% of 3.5 degree slews at elevation less than 60 degrees fail to meet the 4s requirement. Additionally, for a few slews the TMA said it was in position before it actually was. 32% of the 15 second periods after the slews failed the 0.01 jitter requirement. This could be due in part to mount encoder errors. Further analysis needs to be done with the accelerometers and with the StarTracker data to confirm the information coming from the mount encoder.


Methodology
===========

On March 9, 15 and 17, and 23, 2023, we used the following test strategy to check the stability of the TMA under slews.

1. Take 3 images in one location.
2. Move 3.5 degrees on sky in a random direction and take 3 images there.
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

We evaluate the slew and settle performance.  We measure the total amount of time from when MTPtg sends the command to when the TMA is labeled as in position  (there is usually about 0.2 to 0.3 seconds between when the command is sent and when the slew is detected in the mount encoder data). For the first accurate offset test we performed on March 9, the azimuth and elevation changes are:

.. figure:: /_static/Az_1.png
    :name: fig-az-1

    Azimuth positions for first 3.5 degree offset test on March 9, 2023.

.. figure:: /_static/El_1.png
    :name: fig-el-1

    Elevation positions for first 3.5 degree offset test on March 9, 2023.

We then isolate the slew times based on when the mount encoder data shows that azimuth or elevation are changing at a sufficiently fast rate of greater than 0.1 per readout. Here is an example plot for the above test:

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

    And additionally we repeat this for tests on March 17, 2023:

.. figure:: /_static/Az_0317.png
    :name: fig-az-3

    Azimuth positions for a 3.5 degree offset test on March 17, 2023.

.. figure:: /_static/El_0317.png
    :name: fig-el-3

    Elevation positions for a 3.5 degree offset test on March 17, 2023.

.. figure:: /_static/Slew_all_0317.png
    :name: fig-slew-all-3

    Slew times for a 3.5 degree offset test on March 17, 2023.

.. figure:: /_static/Slew_3_5_0317.png
    :name: fig-slew-3.5-3

    Slew times for 3.5 degree slews for the second 3.5 degree offset test on March 17, 2023.


And for tests on March 24, 2023:


.. figure:: /_static/Slew_all_0324.png
    :name: fig-slew-all-3

    Slew times for a 3.5 degree offset test on March 24, 2023.

.. figure:: /_static/Slew_3_5_0324.png
    :name: fig-slew-3.5-3

    Slew times for 3.5 degree slews for the second 3.5 degree offset test on March 24, 2023.


Combined Datasets and Summary
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We combine all the data sets from March 15, March 17, and March 24, for a total of 649 slews, of which 409 are 3.5 degree slews at elevations of less than 60 degrees. Of the 409 slews, 17 have a slew time of 4s or more, so 4.2% fail Sto meet the requirement.

Here is the plot of all 3.5 degree slews:

.. figure:: /_static/Slew_3_5_all.png
    :name: fig-slew-3.5-3

    Slew times for 3.5 degree slews for the second 3.5 degree offset test on March 15, 17,and 24, 2023.

To better understand what is going on, we look at the slew times as a function of azimut and elevation distance:

.. figure:: /_static/Slew_az_el_3_5.png
    :name: fig-slew-3.5-3

    Slew times vs azimuth and elevation slew distance for 3.5 degree slews for the second 3.5 degree offset test on March 15, 17,and 24, 2023.

The outliers with very short slew times correspond to a 45 minute period on the night of the 24th when the mount said it was in position before it actually was.

To fully see what's going on, we plot azimuth slew distance vs elevation, with the color bar corresponding to the slew times. Red x is overlaid on the slews that failed to meet the requirement:

.. figure:: /_static/Slew_all_scatter.png
    :name: fig-slew-3.5-3

    Azimuth slew distance vs elevation, with the color bar corresponding to the slew times. Red x is overlaid on the slews that failed to meet the requirement.

Jitter Tests
------------

For the jitter tests, we look at how much jitter there is for the first 32 seconds after the slew finishes and the first 15 seconds. Specifically, we fit the azimuth and elevation mount encoder data to a fourth order polynomial and then compute the rms of the residuals. A sample plot is shown here:

.. figure:: /_static/jitter_sample.png
    :name: fig-jitter-sample

    Sample jitter plot for one exposure.


We see that there are outliers due to electrical spikes. We remove all points that are 10 :math:`\sigma` outliers and then compute the rms jitter based on that. We then plot the histograms of jitter for all images below.

For the different offset tests, we see:

.. figure:: /_static/jitter_1.png
    :name: fig-jitter-1

    Histogram of the 32 s jitter for the first offset test on March 9, 2023.

.. figure:: /_static/jitter_2.png
    :name: fig-jitter-2

    Histogram of the 32 s jitter for the second offset test on March 9, 2023.

.. figure:: /_static/jitter_3.png
    :name: fig-jitter-3

    Histogram of the 32 s jitter for the offset test on March 15, 2023.

We see that with one exception (which is clearly an outlier), all jitter is less than 0.01 arcsec. However, when we look at 15 seconds, instead of 32 seconds, and also include data from March 17, and March 24, that is no longer the case. In the combined set of data from March 15, 17, and 24, 32% fail to meet the requirement. In part, this is due to what seem to be increased levels of mount encoder jitter, as seen here:

.. figure:: /_static/jitter_example.png
    :name: fig-jitter-3

    Example of jitter from the night of March 24, 2023.

The full distribution looks like this:

.. figure:: /_static/jitter_all.png
    :name: fig-jitter-4

    Histogram of 15 seconds of jitter for the offset tests on March 15, 17, and 24 2023.

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

Slews of 3.5 degrees with elevation less than 60 degrees were completed 96% of the time. 

For the runs on March 15, 17, and 24, the jitter in the 15 seconds after the mount is in position is greater than 0.01 arcsec 32% of the time. This is probably due in part to errors in reading out the mount encoder data, but there may be more fundamental issues.

There may be a ~1 Hz oscillation visible in the fast StarTracker data. We should look at more data and correlate with accelerometer readings to properly do the comparison.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
