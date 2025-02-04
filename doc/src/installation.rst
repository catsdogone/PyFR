.. highlight:: none

************
Installation
************

Quick-start
===========

PyFR |release| can be installed using `pip <https://pypi.python.org/pypi/pip>`_
and `virtualenv <https://pypi.python.org/pypi/virtualenv>`_, as shown in the
quick-start guides below.

Alternatively, PyFR |release| can be installed from
`source <https://github.com/PyFR/PyFR/tree/master>`_, see
:ref:`compile-from-source`.

macOS
-----

We recommend using the package manager `homebrew <https://brew.sh/>`_.
Open the terminal and install the dependencies with the following commands::

    brew install python3 open-mpi metis
    pip3 install virtualenv

For visualisation of results, either install ParaView from the command line::

    brew cask install paraview

or dowload the app from the ParaView `website <https://www.paraview.org/>`_.
Then create a virtual environment and activate it::

    virtualenv --python=python3 ENV3
    source ENV3/bin/activate

Finally install PyFR with `pip <https://pypi.python.org/pypi/pip>`_ in the
virtual environment::

    pip install pyfr

This concludes the installation. In order to run PyFR with the OpenMP backend
(see :ref:`running-pyfr`), use the following settings in the
:ref:`configuration-file`::

    [backend-openmp]
    cc = gcc-8

Note the version of the compiler which must support the ``openmp`` flag.
This has been tested on macOS 10.14.

Ubuntu
------

Open the terminal and install the dependencies with the following commands::

    sudo apt install python3 python3-pip libopenmpi-dev openmpi-bin
    sudo apt install metis libmetis-dev
    pip3 install virtualenv

For visualisation of results, either install ParaView from the command line::

    sudo apt install paraview

or dowload the app from the ParaView `website <https://www.paraview.org/>`_.
Then create a virtual environment and activate it::

    python3 -m virtualenv pyfr-venv
    source pyfr-venv/bin/activate

Finally install PyFR with `pip <https://pypi.python.org/pypi/pip>`_ in the
virtual environment::

    pip install pyfr

This concludes the installation.

This has been tested on Ubuntu 18.04.

.. _compile-from-source:

Compiling from source
=====================

PyFR can be obtained `here <https://github.com/PyFR/PyFR/tree/master>`_.
To install the software from source, use the provided ``setup.py``
installer or add the root PyFR directory to ``PYTHONPATH`` using::

    user@computer ~/PyFR$ export PYTHONPATH=.:$PYTHONPATH

When installing from source, we strongly recommend using
`pip <https://pypi.python.org/pypi/pip>`_ and
`virtualenv <https://pypi.python.org/pypi/virtualenv>`_ to manage the Python
dependencies.

Dependencies
------------

PyFR |release| has a hard dependency on Python 3.6+ and the following
Python packages:

1. `appdirs <https://github.com/ActiveState/appdirs>`_ >= 1.4.0
2. `gimmik <https://github.com/vincentlab/GiMMiK>`_ >= 2.0
3. `h5py <http://www.h5py.org/>`_ >= 2.6
4. `mako <http://www.makotemplates.org/>`_ >= 1.0.0
5. `mpi4py <http://mpi4py.scipy.org/>`_ >= 3.0
6. `numpy <http://www.numpy.org/>`_ >= 1.20
7. `pytools <https://pypi.python.org/pypi/pytools>`_ >= 2016.2.1

Note that due to a bug in NumPy, PyFR is not compatible with 32-bit
Python distributions.

.. _install cuda backend:

CUDA Backend
^^^^^^^^^^^^

The CUDA backend targets NVIDIA GPUs with a compute capability of 3.0
or greater. The backend requires:

1. `CUDA <https://developer.nvidia.com/cuda-downloads>`_ >= 8.0

HIP Backend
^^^^^^^^^^^

The HIP backend targets AMD GPUs which are supported by the ROCm stack.
The backend requires:

1. `ROCm <https://rocmdocs.amd.com/en/latest/>`_ >= 4.0
2. `rocBLAS <https://github.com/ROCmSoftwarePlatform/rocBLAS>`_ >= 2.32.0

OpenCL Backend
^^^^^^^^^^^^^^

The OpenCL backend targets a range of accelerators including GPUs from
AMD, Intel, and NVIDIA. The backend requires:

1. OpenCL
2. `pyopencl <http://mathema.tician.de/software/pyopencl/>`_
   >= 2015.2.4
3. `CLBlast <https://github.com/CNugteren/CLBlast>`_

.. _install openmp backend:

OpenMP Backend
^^^^^^^^^^^^^^

The OpenMP backend targets multi-core CPUs. The backend requires:

1. GCC >= 4.9 or another C compiler with OpenMP support
2. Optionally `libxsmm <https://github.com/hfp/libxsmm>`_ >= commit
   14b6cea61376653b2712e3eefa72b13c5e76e421 compiled as a shared
   library (STATIC=0) with BLAS=0 and CODE_BUF_MAXSIZE=262144

Parallel
^^^^^^^^

To partition meshes for running in parallel it is also necessary to
have one of the following partitioners installed:

1. `METIS <http://glaros.dtc.umn.edu/gkhome/views/metis>`_ >= 5.0
2. `SCOTCH <http://www.labri.fr/perso/pelegrin/scotch/>`_ >= 6.0
