-------------------
HOWTO install S4 permanently on Google Drive and run with Colab NOtebook on Goggle VMs (~Jupyter notebooks)

1) Create the "S4all" program folder on your Gdrive and a "libraries" subfolder (if you want to change the folder name, you will have to edit the Makefile)

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
3) Now cd into the S4 folder and compile it all:
```
%cd S4
!make boost
!make S4_pyext
```





