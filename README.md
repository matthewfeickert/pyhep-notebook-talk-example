# PyHEP Notebook Talk Example

Example repository structure for a PyHEP style "notebook talk"

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)

## Minimum Required Setup

The minimum setup required is simply a repository with the Jupyter notebook that you'll be using and the `requirements.txt` or environment config file that is used to specify and install all of your code's dependencies.
Note that it is rather important to **exactly** specify the requirements with `==` to avoid the repository code breaking in the future.

## Recommended Setup

Ideally, in addition to the minimum requirements, you'll also make the repository runnable on [Binder](https://mybinder.org/).
The easiest way to do this is to simply ensure that _all_ of your dependencies are properly specified in your `requirements.txt` file and then to create a `binder` directory in the top level of the repository and place the `requirements.txt` file in it.
Binder knows to look for configuration files under the `binder` directory so you can put all of your [Binder configuration files](https://mybinder.readthedocs.io/en/latest/config_files.html) there.

Once these requirements have been met and commit to your repository if you visit [mybinder.org](https://mybinder.org/) and paste the URL of your GitHub repostiory (or Zenodo DOI!) into the text box, Binder will generate a badge for your repository README.
If a user just clicks that badge, the Binder build will run if there already isn't a built image for it and then launch the user into an interactive session inside of the image running on Binder Federation resources.

Below is an example of a URL that will launch the `talk.ipynb` notebook in this repository into a JupyterLab environment.

```
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)
```

and its badge

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)

### Jupyter Lab Optional Launcher

If you'd like to have your Binder badge [launch into a JupyterLab environment](https://mybinder.readthedocs.io/en/latest/howto/user_interface.html#jupyterlab) instead of Jupyter Notebook have the URL end with `?urlpath=lab/tree/path-to-the-notebook-you-want.ipynb`.

## Zenodo DOIs

To preserve the repository with your talk as best as possible, have [Zenodo](https://zenodo.org/) build a Zenodo archive and mint a DOI for your repository.
To do this:

1. Create an account on [zenodo.org](https://zenodo.org/).
2. [Follow the instructions](https://zenodo.org/account/settings/github/) on syncing GitHub repositories that you control with Zenodo.
3. Create a new GitHub release to trigger an archive capture.
4. Add the minted DOI to your repository as a badge.

This DOI can then be used by PyHEP to add your Zenodo archive to a PyHEP community colleciton on Zenodo. c.f. [PyHEP 2020's Zenodo community](https://zenodo.org/communities/pyhep2020) as an example.

You can create a Binder launch URL **from a Zenodo DOI** which will build the Docker image from the contents of the Zenodo archive.

## Installation

In a clean virtual environment install the dependencies (which are under the `binder` directory)

```console
python -m pip install -r binder/requirements.txt
```
