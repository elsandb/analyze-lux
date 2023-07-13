# Trying out [LUX](https://lux-api.readthedocs.io/en/latest/) - A Python API for Intelligent Visual Discovery

---
Install lux: 
In terminal: ``py -m pip install lux-api`` (may take a few minutes). Works ✅
---

## (1) Make LUX work in JupyterLab

🐝 **Sum**mary: I didn't manage to use Lux in JupyterLab. 
        Jump to section 2 if the JupyterLab-journey 
        is not interesting. 🐝

When trying to install the LUX JupyterLab-extension with 
``jupyter labextension install @jupyter-widgets/jupyterlab-manager``,
I got this message:

```
(Deprecated) Installing extensions with the jupyter labextension install command is now deprecated and will be removed in a future major version of JupyterLab.

Users should manage prebuilt extensions with package managers like pip and conda, and extension authors are encouraged to distribute their extensions as prebuilt packages
An error occurred.
ValueError: Please install Node.js and npm before continuing installation. You may be able to install Node.js from your package manager, from conda, or directly from the Node.js website (https://nodejs.org).
See the log file for details:  C:\Users\Bruker\AppData\Local\Temp\jupyterlab-debug-oec700jt.log
```

Because of the message above, I downloaded nodejs (the version labeled 
"recommended for most users"). When asked if I want to install Tools for 
Native Modules, I checked of for "Automatically install necessary tools...". 
After the wizard was done, the 'Install Additional Tools for Node.js'-window showed up:

```
====================================================
Tools for Node.js Native Modules Installation Script
====================================================

This script will install Python and the Visual Studio Build Tools, necessary
to compile Node.js native modules. Note that Chocolatey and required Windows
updates will also be installed.

This will require about 3 GiB of free disk space, plus any space necessary to
install Windows updates. This will take a while to run.

Please close all open programs for the duration of the installation. If the
installation fails, please ensure Windows is fully updated, reboot your
computer and try to run this again. This script can be found in the
Start menu under Node.js.

You can close this window to stop now. Detailed instructions to install these
tools manually are available at https://github.com/nodejs/node-gyp#on-windows

Press any key to continue . . .
```
I chose to close the window, because I didn't want to spend so much time and 
storage space before I know if it is actually necessary.


In terminal and JupyterLab, I tried 
``jupyter labextension install @jupyter-widgets/jupyterlab-manager`` 
again as well as ``jupyter labextension install luxwidget``, but the same 
error message as before showed up.

**Conclusion: I give up to use Lux in JupyterLab**

---

## (2) Make LUX work in Jupyter notebook
🐝 **Sum**mary: Using Lux in Jupyter notebook worked fine.
See notebook ``start_lux.ipynb``. 🐝

I opened jupyter notebook from Anaconda Navigator (desktop UI), 
with 'venv_lux' activated. I installed pandas from Anaconda 
Navigator, and LUX from the notebook (se comments and code below or 
in the notebook).

````python
    --- In jupyter notebook ---

    # Check that the notebook is using the correct venv.
    import sys
    print('Path to active virtual environment: ', sys.executable)
    # >> Path to active virtual environment:  C:\Users\Bruker\miniconda3\envs\venv_lux\python.exe
    
    import lux
    # Install lux widget:
    !jupyter nbextension install --py luxwidget
    # >> ... lots of text ... 
    # >>    - Validating: ok
    
    # Enable lux widget for jupyter notebook:
    !jupyter nbextension enable --py luxwidget
    # >> Enabling notebook extension luxwidget/extension...
    # >>    - Validating: ok    

    # Debug lux widget if needed:
    # lux.debug_info()
````

lux-api                  0.5.1
lux-widget               0.1.11

## (3) The LUX basics

**Required imports:** 
````python
import pandas as pd
import lux
````

**Set Lux as default display:** `df.default_display = "lux"`. 
Note: This is pretty annoying if you want to process the dataframe 
before displaying the charts.

**Get started:** Read in a .csv file and let LUX do its thing.

````python
# Example:
df = pd.read_csv('./data/example.csv')
df['Date'] = pd.to_datetime(df['Date'], format='%Y-%m-%d')
df
````

