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

We evaluate the slew and settle performance by 

Jitter Tests
------------



Summary
=======




.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
