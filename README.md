# Windows Embeddable Python with virtualenv support

The repository contains code to repackage Windows Embeddable version of Python with virtualenv.

## What is Windows Embeddable Python?

Windows Embeddable Python is a minimalistic Python distribution suitable for bundling Python inside applications for Windows.

The package is stored in downloads: https://www.python.org/downloads

The name of the package is: Windows x86-64 embeddable zip file

## Why is it necessary to repackage ZIP with Embeddable Python?

The official version has the following limitations:
* the package does not contain pip
* the package does not support virtualenv
* resolution of module path behaves slightly different
    * more details: https://dev.to/fpim/setting-up-python-s-windows-embeddable-distribution-properly-1081

## How it works

* download and unpack Windows Embeddable Python
* extract content of pythonYY.zip to Lib, remove pythonYY.zip
* remove pythonYY._pth file
    * this file controls behavior of imports when starting Python
* download get-pip.py and install pip
* pip install virtualenv
* download or use full version of python and copy Lib\\venv\\scripts\\nt\\*.exe to python bundle
    * during the creation of virtualenv these python.exe and pythonw.exe files are being copied to virtual environment location
    * these two files are different from python.exe and pythonw.exe in the top Python directory

## How to build

PowerShell:
```
.\Bundle-Python.ps1 -PythonVersion 3.8.6
```

Result Python distribution will be available in python directory.

### How to build with GitHub Actions

Check the version of Python in ```.github/workflow/bundle-python.yaml```.
Commit the change and check Actions at GitHub.com.
Zip file with the result will be available as artifact in build details.
