.. image:: https://travis-ci.org/jeremiedecock/pywi-cta.svg?branch=master
    :target: https://travis-ci.org/jeremiedecock/pywi-cta

=================================
PyWI CTA - A CTA wrapper for PyWI
=================================

Copyright (c) 2016-2018 Jeremie DECOCK (www.jdhp.org)

* Web site: http://cta.pywi.org/
* Online documentation: http://cta.pywi.org/docs/
* Source code: https://github.com/jeremiedecock/pywi-cta
* Issue tracker: https://github.com/jeremiedecock/pywi-cta/issues
* PyWI-CTA on PyPI: https://pypi.org/project/pywicta/
* PyWI-CTA on Anaconda Cloud: https://anaconda.org/jdhp/pywicta

.. Former documentation: http://sap-cta-data-pipeline.readthedocs.io/en/latest/

.. Former documentation: https://jeremiedecock.github.io/pywi-cta/

Description
===========

PyWI-CTA is a ctapipe_ wrapper for PyWI_.

.. warning::

    This project is in beta stage.

Features
========

The PyWI and PyWI-CTA libraries contain:

* wavelet transform and wavelet filtering functions for image multiresolution
  analysis and filtering;
* additional filter to remove some image components (non-significant pixels
  clusters);
* a set of generic filtering performance estimators (MSE, angular precision,
  energy loss, contamination rate, ...), some relying on the scikit-image
  Python library (supplementary estimators can be easily added to meet
  particular needs);
* a graphical user interface to visualize the filtering process in the wavelet
  transformed space;
* an Evolution Strategies (ES) algorithm known in the mathematical optimization
  community for its good convergence rate on generic derivative-free continuous
  global optimization problems (Beyer, H. G. (2013) "The theory of evolution
  strategies", Springer Science & Business Media);
* additional tools to manage and monitor the parameter optimization.

Dependencies
============

.. Highly inspired by http://docs.astropy.org/en/stable/_sources/install.rst.txt

PyWI-CTA has the following strict requirements:

* `Python <https://www.python.org/>`_ 3.5 or 3.6
* `Numpy <http://www.numpy.org/>`_
* ctapipe_ 0.6.1
* pyhessio 2.0.1

PyWI-CTA also depends on other packages for optional features:

* `Scipy <https://www.scipy.org/>`_
* `Scikit-image <http://scikit-image.org/>`_
* `Pillow (a.k.a. PIL) <https://pillow.readthedocs.io/en/latest/>`_ to read and write many image formats (PNG, JPEG, TIFF, ...)
* `Astropy <http://www.astropy.org/>`_ to provide Fits file format
* `Pandas <http://pandas.pydata.org/>`_
* `Matplotlib <http://matplotlib.org/>`_ 1.5 or later to provide plotting functionality
* PyWI_
* `Cosmostat iSAP Sparce2D <http://www.cosmostat.org/software/isap/>`_

However, note that these only need to be installed if those particular features
are needed. `pywicta` will import even if these dependencies are not installed.

.. _install:

Installation
============

PyWI-CTA and its dependencies may be installed using the *Anaconda* or
*Miniconda* package system. We recommend creating a conda virtual environment
first, to isolate the installed version and dependencies from your master
environment (this is optional).

The following command will set up a conda virtual environment, add the
necessary package channels, and download PyWI-CTA and its dependencies. The
file *environment.yml* can be found in this repository. 
Note this is *beta* stage software and is not yet stable enough for end-users
(expect large API changes until the first stable 1.0 release).

::

    conda env create -n pywi-cta -f environment.yml
    source activate pywi-cta
    pip install pywicta --no-deps

If you have already installed *ctapipe* following the
`official installation procedure <https://github.com/cta-observatory/ctapipe#installation-for-users>`_,
you can add PyWI-CTA to the *cta* virtual environment like this::

    source activate cta
    pip install pywicta --no-deps

Developers should follow the development install instructions found in the
`documentation <https://jeremiedecock.github.io/pywi-cta/developer.html#getting-started-for-developers>`_.

.. note::

    As *ctapipe* is not tested to work on Microsoft Windows systems, PyWI-CTA
    does not officially support these systems neither.

.. note::

    The ``--no-deps`` flag is optional, but highly recommended otherwise pip
    will sometimes try to "help" you by upgrading PyWI-CTA dependencies like
    Numpy, which may not always be desired.

Cosmostat iSAP Sparce2D installation (optional)
===============================================

1. Download http://www.cosmostat.org/wp-content/uploads/2014/12/ISAP_V3.1.tgz (see http://www.cosmostat.org/software/isap/)
2. Unzip this archive, go to the "sparse2d" directory and compile the sparse2d
   library. It should generate two executables named ``mr_transform`` and ``mr_filter``::

    tar -xzvf ISAP_V3.1.tgz
    cd ISAP_V3.1/cxx
    tar -xzvf sparse2d_V1.1.tgz
    cd sparse2d
    compile the content of this directory

An automated compilation and installation script for Linux is available
`here <https://github.com/tino-michael/tino_cta/blob/master/grid/compile_mrfilter_pilot.sh>`_
(author: `Tino Michael <https://github.com/tino-michael>`_).

.. Also available in `utils/compile_isap_sparce2d.sh`

Getting started: tutorial Notebooks
===================================

PyWI-CTA provides some Jupyter notebooks that can be used as examples or tutorials: https://github.com/jeremiedecock/pywi-cta-notebooks.
New users should check them in the following order:

* Tutorial #0:  `Check PyWI-CTA install <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_0_check_install.ipynb>`_
* Tutorial #1a: `Load and plot a FITS image using PyWI-CTA <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_1a_load_and_plot_fits_image.ipynb>`_
* Tutorial #1b: `Load and plot a Simtel event using PyHESSIO <https://nbviewer.jupyter.org/github/jeremiedecock/pywi-cta-notebooks/blob/master/tuto_1b_load_simtel_event.ipynb>`_
* Tutorial #1c: `Load and plot a Simtel image using PyWI-CTA <https://nbviewer.jupyter.org/github/jeremiedecock/pywi-cta-notebooks/blob/master/tuto_1c_load_and_plot_simtel_image.ipynb>`_
* Tutorial #1d: `Plot Hillas parameters using PyWI-CTA <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_1d_plot_hillas_parameters.ipynb>`_
* Tutorial #2a: `Tailcut cleaning with PyWI-CTA <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_2a_tailcut_cleaning.ipynb>`_
* Tutorial #2b: `Plot Starlet planes with PyWI-CTA <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_2b_plot_starlet_planes.ipynb>`_
* Tutorial #2c: `Starlet cleaning with PyWI-CTA <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_2c_starlet_cleaning.ipynb>`_
* Tutorial #3a: `Tailcut interactive notebook <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_3a_interactive_tailcut_cleaning_with_bokeh.ipynb>`_
* Tutorial #3b: `Starlet cleaning interactive notebook <https://mybinder.org/v2/gh/jeremiedecock/pywi-cta-notebooks/master?filepath=tuto_3b_interactive_starlet_cleaning_with_bokeh.ipynb>`_
* Tutorial #3c: `Wavelet Sparce2D MrTransform interactive notebook <https://nbviewer.jupyter.org/github/jeremiedecock/pywi-cta-notebooks/blob/master/tuto_3c_interactive_mrtransform_cleaning_with_bokeh.ipynb>`_

.. PyWI Notebooks on Anaconda Cloud: https://anaconda.org/jdhp/notebooks

Console usage example
=====================

PyWI-CTA can also be used through console commands. The following is an usage example:

1. Get a simtel file (e.g. from `there <https://forge.in2p3.fr/projects/cta_analysis-and-simulations/wiki/Monte_Carlo_Productions>`_)
2. In your system terminal, from the directory that contains the sample image,
   type the following commands (where `SIMTEL_FILE` is the path to your simtel
   file)::
  
    pywicta-starlet -f common_hard_filtering -t 13.,1.5 -L mask --camid LSTCam --max-images 1 --plot SIMTEL_FILE
    pywicta-mrtransform -f common_hard_filtering -t 13.,1.5 -L mask --camid LSTCam --max-images 1 --plot SIMTEL_FILE
    pywicta-mrfilter -K -k -C1 -m3 -n4 -s2,4.5,3.5,3 --kill-isolated-pixels --camid LSTCam --max-images 1 --plot SIMTEL_FILE

3. Type ``pywicta-starlet -h``, ``pywicta-mrtransform -h`` or ``pywicta-mrfilter -h`` to display the list of
   available options and their documentation.

.. A "benchmark mode" can also be used to clean images and assess cleaning
.. algorithms (it's still a bit experimental): use the additional option ``-b all``
.. in each command (and put several fits files in input e.g. ``\*.fits``)

Analysis results
================

Notebooks containing the analysis results can be found there: https://gitlab.com/jdhp/pywi-cta-analysis

* `LST analysis (essential plots) <https://mybinder.org/v2/gl/jdhp%2Fpywi-cta-analysis/master?filepath=cta_analysis_lst_essential.ipynb>`_
* `LST analysis (very detailed) <https://mybinder.org/v2/gl/jdhp%2Fpywi-cta-analysis/master?filepath=cta_analysis_lst.ipynb>`_

Bug reports
===========

To search for bugs or report them, please use the PyWI Bug Tracker at:

    https://github.com/jeremiedecock/pywi-cta/issues


.. _PyWI: http://www.pywi.org/
.. _ctapipe: https://github.com/cta-observatory/ctapipe
.. _command prompt: https://en.wikipedia.org/wiki/Cmd.exe
