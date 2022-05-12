-------------------
HOWTO install S4 permanently on Google Drive and run it with Colab Notebook on free Google VMs (~Jupyter notebooks)

1) Create the "S4all" program folder on your Gdrive and a "libraries" subfolder (if you want to change the folder name, you will have to edit the Makefile)

2) Open an empty Colab notebook, type this and run (Google will ask your permission to access your Drive, grant it):
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
3) cd into the S4_xColab folder and compile it all (please grab a drink, this will take "some" time):
```
%cd S4_xColab
!make boost
!make S4_pyext
```
4) S4_xColab is now permanently installed on your Google Drive. To create a simulation, create a new Colab Notebook with the following heading cell, followed by :
```
from google.colab import drive
import os, sys
drive.mount('/content/gdrive')
%cd /content/gdrive/MyDrive/S4all
lib_path = '/content/gdrive/MyDrive/S4all/libraries'
sys.path.insert(0,lib_path)

!apt-get install libopenblas-dev libfftw3-dev libsuitesparse-dev

import S4
```
4bis) Mind that your will be asked to grant access to drive and to reinstall blas and fftw libraries every time you disconnect your Colab Notebook; this normally happens automatically after some minutes of inactivity, so you'd better trick Google into thinking that you are always active while the Notebook is open; you can do that adding this line in a cell following your whole code:
```
while True:pass
```






