Available Software:
-------------------

Native system:
~~~~~~~~~~~~~~

All of the submit machines come with several tools to help you get started with your work. A few examples are shown below:

1. Languages:

- python

- c++

- Java

2. Tools:

- XRootd

- GFAL

For more complicated workflows, there are several options on how to proceed. Many environments can be set up through CVFMS provided by CERN. If you need more control of the environment, either conda or dockers are commonly used and well supported. For more information see the sectiosns below.

CVMFS:
~~~~~~

The CernVM File System (CVMFS) provides a scalable, reliable and low- maintenance software distribution service. It was developed to assist High Energy Physics (HEP) collaborations to deploy software on the worldwide- distributed computing infrastructure used to run data processing applications. CernVM-FS is implemented as a POSIX read-only file system in user space (a FUSE module). Files and directories are hosted on standard web servers and mounted in the universal namespace /cvmfs.

More documentation on CVMFS can be found here:

#. `CVMFS <https://cernvm.cern.ch/fs/>`_

In order to initialize CVMFS on submit machines you can simply use the command below:

.. code-block:: sh

      source /cvmfs/cms.cern.ch/cmsset_default.sh

Once CVMFS has been sourced you can see the options in /cvmfs. If you want to use ROOT or any other CMS specific tools you can also download CMSSW releases and work within a CMS environment. A simple example is shown below:

.. code-block:: sh

      cmsrel CMSSW_10_2_13
      cd CMSSW_10_2_13/src
      cmsenv

Once the cms environment is set up, ROOT is now available to you as well

Conda:
~~~~~~

Conda is an open source package management system and environment management system. We can use this to set up consistent environments and manage the package dependencies for various applications. Below is an example to set up a python3 environment for working with coffea and dask. 

### Coffea installation with Miniconda
For installing Miniconda, see also https://hackmd.io/GkiNxag0TUmHnnCiqdND1Q#Local-or-remote

.. code-block:: sh

      wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
      # Run and follow instructions on screen
      bash Miniconda3-latest-Linux-x86_64.sh

NOTE: always make sure that conda, python, and pip point to local Miniconda installation (`which conda` etc.).

You can either use the default environment`base` or create a new one:

.. code-block:: sh

      # create new environment with python 3.7, e.g. environment of name `coffea`
      conda create --name coffea python=3.7
      # activate environment `coffea`
      conda activate coffea

Install coffea, xrootd, and more. SUEP analysis uses Fastjet with awkward array input (fastjet>=3.3.4.0rc8) and vector:


.. code-block:: sh

      pip install git+https://github.com/CoffeaTeam/coffea.git #latest published release with `pip install coffea`
      conda install -c conda-forge xrootd
      conda install -c conda-forge ca-certificates
      conda install -c conda-forge ca-policy-lcg
      conda install -c conda-forge dask-jobqueue
      conda install -c anaconda bokeh 
      conda install -c conda-forge 'fsspec>=0.3.3'
      conda install dask
      conda install pytables
      pip install --pre fastjet
      pip install vector


Containers:
~~~~~~~~~~~

