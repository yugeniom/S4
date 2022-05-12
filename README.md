-------------------
HOWTO install S4 permanently on Google Drive and run with Colab NOtebook on Goggle VMs (~Jupyter notebooks)

1) Create the "S4all" program folder on your Gdrive (if you want to change the folder name, you will have to edit the Makefile)

2) Open an empty Colab notebook and type this:
```
from google.colab import drive
import os, sys
drive.mount('/content/gdrive')
%cd /content/gdrive/MyDrive/S4all
lib_path = '/content/gdrive/MyDrive/S4all/libraries'
sys.path.insert(0,lib_path)

!apt install make git gcc g++ gfortran
!apt-get install libopenblas-dev libfftw3-dev libsuitesparse-dev

!pip3 install wheel setuptools numpy scipy matplotlib
```

2) Clone this repository, typing in a new cell:
```
git clone https://github.com/yugeniom/S4_xColab.git
```
3) Now cd into the S4 folder:





If you are looking for a more user-friendly interface to S4 (wavelength-dependent calculations, material management etc.), check out my Python3 package [RayFlare](https://rayflare.readthedocs.io)

# Installation instructions (64-bit Ubuntu 16/18/20 or MacOS):

## Key steps:

```
git clone https://github.com/phoebe-p/S4
cd S4
make S4_pyext
```

Running the `make boost` command before `make S4_pyext` should automatically download and compile the relevant Boost libraries in the local S4 directory. 
HOWEVER, this appears to cause problems on macOS, so if you are installing on macOS you should install the boost libraries 
using Homebrew (see below). If you want to use Boost libraries in a different location you will have to edit the Makefile.

**Note for users of new (late 2020 onwards) Apple machines with M1/Apple silicon/ARM chips: you will need to use Makefile.m1
to compile successfully, see notes below on how to do this.**

## Installing relevant libraries etc.:

**On Ubuntu (with a working version of Python3):**

```
sudo apt-get update
sudo apt install make git gcc g++
sudo apt install libopenblas-dev libfftw3-dev libsuitesparse-dev
```

- libopenblas installs OpenBLAS, to satisfy the LAPACK and BLAS requirements
- lib fftw3 install FFTW3, to satisfy the FFTW requirements
- libsuitesparse install libraries to satisdy CHOLMOD & related requirements

If you want, you can also install the boost libraries using `sudo apt install libboost-all-dev` instead of running `make boost`.

**On MacOS using Homebrew:**

```
brew install fftw suite-sparse openblas lapack boost
```

You can get the make and git commands from homebrew, or through Apple Developer Tools. If the packages are installed/symlinked by Homebrew to the default location (/usr/local/include) you should not have to modify the Makefile, and you should be able to use the same Makefile as Ubuntu/Linux (i.e. no need to use Makefile.osx).

*If you have multiple Python versions, you may need to modify the S4_pyext part of the Makefile:*

````
pip3 install --upgrade ./
````

to e.g.:
```
[path of target python or virtual environment] setup.py install
```

You can install S4 into a virtual environment automatically by just activating that environment in your terminal before running `make S4_pyext`.

See [here](https://rayflare.readthedocs.io/en/latest/Installation/installation.html) for more extensive instructions.


**On MacOS with M1/ARM chips:**

Some of the flags used in the default Makefile cause issues with the new chip architecture. Run the following instead:

```
git clone https://github.com/phoebe-p/S4
cd S4
make S4_pyext --file="Makefile.m1"
```

Installing the libraries with Homebrew should work as expected.

-------------------------------------

S4: Stanford Stratified Structure Solver (http://fan.group.stanford.edu/S4/)

A program for computing electromagnetic fields in periodic, layered
structures, developed by Victor Liu (victorliu@alumni.stanford.edu) of the
Fan group in the Stanford Electrical Engineering Department.

See the S4 manual, in doc/index.html, for a complete
description of the package and its user interface, as well as
installation instructions, the license and copyright, contact
addresses, and other important information.

---------------------------------------

sajidmc: The MakefileHPC is created to compile the S4 in HPC environment without
root access. Also added an example for python extension testing: 

Check Wiki for details: https://github.com/sajidmc/S4/wiki
Example result: https://raw.githubusercontent.com/sajidmc/S4/master/examples/bontempi_et_al_Nanoscale_2017.png

