# Virtual Environment & Pip   

### Virtural Environemnet   

It is best to make a virtual environment for every new project, since some libaries, if installed togther can create conflict. Installing
them on system python is NOT a good move.

#### Creating venv for windows/linux:
```
python3 -m venv <path-of-installation>
```   

#### Activating venv on windows:
```
<path-of-installation>\env\Scripts\activate
```   

#### Activating venv on linux:
```
source <path-of-installation>/env/bin/activate
```

### Pip
    
It's package manager for python.

#### Install rrequirenment from requirement.txt:   
```
pip install -r requirements.txt
```
    
#### Install a module from .zip
```
< Extract the .zip and Cd into the folder, install requirenments >
python setup.py install
```

Everything about pip is [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)
