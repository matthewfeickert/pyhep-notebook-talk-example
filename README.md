# PyHEP Notebook Talk Example

Example repository structure for a PyHEP style "notebook talk"

## Minimum Required Setup

The minimum setup required is simply a repository with the Jupyter notebook that you'll be using and the `requirements.txt` or environment config file that is used to specify and install all of your code's dependencies.
Note that it is rather important to **exactly** specify the requirements with `==` to avoid the repository code breaking in the future.

## Recommended Setup

## Installation

First in a clean virtual environment install the dependencies (which are under the `binder` directory)

```console
python -m pip install -r binder/requirements.txt
```
