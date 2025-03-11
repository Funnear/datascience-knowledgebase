# Developer setup for Python + Jupyter Notebook project

## Virtual environment management

Create one virtual environment for each project and use it in Jupyter as well as in terminal for executing plain Python scripts (including tests) and package management.

### For Mac/Linux users

Create the virtual environment: 
```bash
python3 -m venv venv
```

Activate the virtual environment:
```bash
source venv/bin/activate
```

Deactivate to switch back to normal terminal usage or activate another virtual environment to work with another project run:
```bash
deactivate
```

[optional] Set alias for venv:
TODO

### Configure using the same environment for Jupyter Notebooks

Preconditions: install dependencies first (see package management), including `ipykernel`!

After running this comand in terminal:
```bash
python -m ipykernel install --user --name=venv --display-name "Python (venv)"
```
restart VS code.

Open a `.ipynb` file and add code block at the top with:
```python
!which python
```

Try running the cell. VS Code will prompt for choosing a Jupyter kernel:
- Select another kernel
- Jupyter kernel
- *Refresh the list using icon on the top right!*
- Choose the virtual environment of this project.

Run the code cell again and make sure it returns the correct path to `<this project folder>/venv/bin/python3`

This will resolve all possible `ModuleNotFoundError` occurences when importing libraries.


----------------------------------------

## Package management: classic way

### External dependencies

Sample requirement.txt contents for data science project:
```bash
jupyterlab>=4.3.5
ipykernel>=6.29.5
pandas>=2.2.2
kagglehub>=0.3.10
numpy>=1.26.4
matplotlib>=3.9.2
seaborn>=0.13.2
matplotlib-venn>=1.1.2
statsmodels>=0.14.4
```

```bash
pip install --upgrade pip; \
pip install -r requirements.txt
```

### Local packages and modules

Create and modify custom Python scripts to use inside Jupyter Notebooks in the same git repo.

Project file structure:
```
project_name/
│── libs/                      # Submodules will be imported here (see below)
│── package_name/              # Main package directory
│   ├── __init__.py            # Makes it a package
│   ├── module_name_1.py         # Example module
│   ├── module_name_2.py       # Example module
│── tests/                     # Test scripts
│   ├── test_module_name_1.py    # Separate test scripts for each module
│   ├── test_module_name_2.py    # Separate test scripts for each module
│── notebooks/                 # Jupyter notebooks
│── .gitignore                 # Auto-generate here: https://www.toptal.com/developers/gitignore
│── README.md                  # Documentation in Markdown format
│── requirements.txt           # Dependencies
│── setup.py                   # Optional for local installation
│── pyproject.toml             # Optional if you use Poetry
│── LICENSE                    # License text

```

These files are key things that must be created to convert python scripts into a package with modules:
- `__init__.py`: can be empty or contain preloaded modules and functions
- `setup.py`: sample content:

```python
from setuptools import setup, find_packages

setup(
    name="package_name",
    version="0.0.1",
    packages=find_packages(),
)
```

To install the local package run this in activated virtual environment:
```bash
pip install -e .
```

### Git submodules

Use this to use and modify custom Python scripts from another git repository.

Link submodule:
```bash
git submodule add https://github.com/user_name/project_name.git libs/project_name; \
git submodule update --init --recursive
```

Install as local package in activated venv:
```bash
pip install -e ./libs/project_name
```

To import submodule  add and run this code from inside a python script or a Jupyter notebook:

```python
import sys
import os

# Get absolute path to the module
module_path = os.path.abspath("./libs")

# Add the directory to sys.path 
if module_path not in sys.path:
    sys.path.append(module_path)
```

After this you will be able to import the entire package or any module, class method from it:
```python
from submodule_package_name.module_name import some_function
# OR:
import submodule_package_name.module_name as utils
```


#### Update submodule

Do this to sync the changes to the original repo of the submodule:
```bash
git submodule update --remote --merge
```

#### Remove submodule
```bash
git rm --cached libs/package_name
rm -rf .git/modules/libs/package_name
git commit -m "Removed submodule"
```

----------------------------------------

## Package managemement: Poetry (.toml)

This method is not recommended for using with editable submodules imported in jupyter Notebooks.

Poetry (pyproject.toml)

### Kick start
```bash
pip install poetry
```

Inside the project folder:
```bash
poetry init
```
- this will require manual inputs.

if there are requirements for pip:
```bash
poetry add $(cat requirements.txt)
```

If you want to use Poetry only for dependency management but not for packaging, 
you can disable package mode by setting `package-mode = false` in your pyproject.toml file.

create venv:
```bash
poetry install; \
poetry env use python3
```

VS Code needs to know about the Poetry envs from PATH:
```bash
poetry env info --path
```

VS Code command pallete -> Open User Settings (JSON) -> copy the output from the previous command to add line:
```
"python.venvPath": "/Users/user_name/Library/Caches/pypoetry/virtualenvs"
```

### Regular usage

To activate virtual environment:
```bash
poetry env activate
```

Add library:
```bash
poetry add scipy
```

### Maintenance

```bash
poetry update; \
poetry export -f requirements.txt --output requirements.txt
```

TODO: make a shell script
```bash
#!/bin/bash
poetry update && poetry export -f requirements.txt --output requirements.txt
git add pyproject.toml poetry.lock requirements.txt
git commit -m "Updated dependencies"
git push origin main
```


