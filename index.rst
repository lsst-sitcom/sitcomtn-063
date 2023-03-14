:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

Checks the performance of the TMA under 3.5 degree random offsets tracking for 32 seconds (and back to original position) in the full range of azimuth and elevation (another az-el grid).  Checks repeatability, jitter, slew and settle against encoders in EFD, star trackers, and accelerometers. Requirements that must be met are documented in LTS 103. 


Methodology
===========

On March 9, 2023, we used the following test strategy to check the stability of the TMA under slews.

1. Take 3 images in one location.
2. Move 3.5 degrees in a random direction and take 3 images there.
3. Return to location (1) and take three more images.
4. Repeat steps 2 and 3 four more times.
5. Move to new location and repeat steps 1 – 4.

Analysis
========

For each central location we plot:

1. The ra and dec of all images in the set.
2. The ra and dec offset for the central position relative to the first image taken (without wcs). Different colors correspond to different repetitions in step 3.
3. The calculated ra and dec offset of the central position relative to the first image taken (with wcs). Different colors correspond to different repetitions in step 3.

We also calculate the drift and jitter in ra and dec over time.


Summary
=======




.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
