# PyHEP Notebook Talk Example

Example repository structure for a PyHEP style "notebook talk"

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)
[![DOI](https://zenodo.org/badge/381276327.svg)](https://zenodo.org/badge/latestdoi/381276327)

> N.B.: If you have questions on how to build a notebook talk, or the instructions below for sharing your notebook talk with Binder and preserving it with Zenodo please ask in the [GitHub Discussions](https://github.com/matthewfeickert/pyhep-notebook-talk-example/discussions)!

## Presentation Resources

> **PyHEP 2025 Update:** PyHEP 2025 will be using a BinderHub that has been deployed by IRIS-HEP's [Scalable Systems Laboratory](https://iris-hep.org/ssl.html) (SSL) at https://binderhub.ssl-hep.org/ which requires authentication with CILogon.
> The instructions are the same as from previous years, with the exception of all urls that use `mybinder.org` will now use `binderhub.ssl-hep.org`.
> A walkthrough video of the workflow is also [available on the HSF YouTube channel](https://youtu.be/4D6eYHNQip0).
>
> **N.B.:** The CILogon identity providers that will work for the SSL BinderHub are verified institutions with signed agreements.
> This means that CERN and any university will work, but Google and GitHub may not.
> If you do not have an affiliation with a verified institution you won't be able to use the SSL BinderHub but you can follow along on the public mybinder BinderHub at http://mybinder.org/.

Before getting into the specifics of how to setup a repository to make it runnable with Binder and preservable with Zenodo, it is a good idea to first think about how to give a talk with a Jupyter notebook.
[Jim Pivarski](https://github.com/jpivarski) has a very good June 2021 PyHEP Topical meeting talk all about things to think about and consider when giving a talk with a Jupyter notebook: [How to give a good Jupyter talk](https://indico.cern.ch/event/1044648/).

## Interactivity with Binder

### Minimum Required Setup (not recommended)

The minimum setup required is simply a repository with the Jupyter notebook that you'll be using and the environment config file (either conda `environment.yaml` or Python `requirements.txt`) that is used to specify and install all of your code's dependencies.
Note that it is rather important to **exactly** specify the requirements with `==` to avoid the repository code breaking in the future.

### Recommended Setup

We strongly recommend that you use [Pixi](https://pixi.sh/)!

Ideally, in addition to the minimum requirements, you'll also make the repository runnable on [Binder](https://mybinder.org/).

The easiest way to do this is to simply ensure that you have a Pixi manifest with _all_ of your dependencies defined in the `default` environment and then to create a `binder` directory in the top level of the repository and create a `binder/runtime.txt` that matches your Python version and then copy the example `binder/postBuild` in this repository.

```
curl -sL https://raw.githubusercontent.com/matthewfeickert/pyhep-notebook-talk-example/refs/heads/main/binder/postBuild -o binder/postBuild
```

> [!CAUTION]
> As of [October 2025](https://github.com/jupyterhub/repo2docker/releases/tag/2025.08.0), `repo2docker`, which underpins Binder, does not have Python 3.13+ support.
> So the most modern Python `binder/runtime.txt` is
> ```
> python-3.12
> ```

Binder knows to look for configuration files under the `binder` directory so you can put all of your [Binder configuration files](https://mybinder.readthedocs.io/en/latest/examples/sample_repos.html) there.
Additionally, specifying the version of Python that should be used to run the code in a `runtime.txt` file under the `binder` directory is useful.

> [!CAUTION]
> The `binder/postBuild` system implemented here **requires** that all dependencies are conda packages.
> If you have dependencies that **only** exist as Python packages (sdists, wheels, or source installs) then you will need to add a line to the end of `binder/postBuild` that manually installs them (ideally from a top level `requirements.txt` file where they are pinned).
> e.g.
> ```bash
> ...
>
> python -m pip install -r ./requirements.txt
> ```

Once these requirements have been met and commit to your repository if you visit [binderhub.ssl-hep.org](https://binderhub.ssl-hep.org/) and paste the URL of your GitHub repository (or Zenodo DOI!) into the text box, Binder will generate a badge for your repository README.
If a user just clicks that badge, the Binder build will run if there already isn't a built image for it and then launch the user into an interactive session inside of the image running on Binder Federation resources.

Below is an example of a URL that will launch the `talk.ipynb` notebook in this repository into a JupyterLab environment.

```
https://binderhub.ssl-hep.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb
```

and its badge

[![Binder](https://mybinder.org/badge_logo.svg)](https://binderhub.ssl-hep.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)

#### Jupyter Lab file browser visible at launch

By default if you provide a path for a notebook to open to BinderHub it will launch it in a "`labpath`" view [JupyterLab environment](https://mybinder.readthedocs.io/en/latest/howto/user_interface.html#jupyterlab) with the notebook as the only view (the JupyterLab file browser will be minimized) and the URL will end with `?labpath=path-to-the-notebook-you-want.ipynb`.
If you would like to have the JupyterLab browser be visible by default you can use instead a `urlpath` view and end the URL with `?urlpath=lab/tree/path-to-the-notebook-you-want.ipynb`

## Local Testing

To test your Binderized setup locally you can use the [`repo2docker`](https://github.com/jupyterhub/repo2docker) command line utility.
Install `jupyter-repo2docker` either [from conda-forge](https://github.com/conda-forge/jupyter-repo2docker-feedstock)

```
pixi global install jupyter-repo2docker
```

or [from PyPI](https://pypi.org/project/jupyter-repo2docker/)

```
uv pip install --upgrade jupyter-repo2docker
```

and then either point `repo2docker` at your local directory

```
repo2docker .
```

or point `repo2docker` to a Git URL for the repository

```
repo2docker <Git repository URL>
```

See

```
repo2docker --help
```

for more information.

BinderHub uses `repo2docker` under the hood to provide the build functionality.

## Zenodo DOIs

### Recommended System: Preservation with Binder support

To preserve the repository with your talk as best as possible, have [Zenodo](https://zenodo.org/) build a Zenodo archive and mint a DOI for your repository.
To do this:

1. Create an account on [zenodo.org](https://zenodo.org/).
2. [Follow the instructions](https://zenodo.org/account/settings/github/) on syncing GitHub repositories that you control with Zenodo.
3. Create a new GitHub release (e.g. "pyhep-2025) to trigger an archive capture.
4. Add the minted DOI to your repository as a badge.

This DOI can then be used by the PyHEP workshop organizers to add your Zenodo archive to the relevant PyHEP community collection on Zenodo, namely [PyHEP 2025's Zenodo community](https://zenodo.org/communities/pyhep2025).

You can create a Binder launch URL **from a Zenodo DOI** which will build the Docker image from the contents of the Zenodo archive.

The following URL and badge will launch a Binder session built from the Zenodo archive

```
https://binderhub.ssl-hep.org/v2/zenodo/10.5281/zenodo.5041728/?urlpath=lab/tree/talk.ipynb
```

[![Binder](https://mybinder.org/badge_logo.svg)](https://binderhub.ssl-hep.org/v2/zenodo/10.5281/zenodo.5041728/?urlpath=lab/tree/talk.ipynb)

Once talks are published, the Zenodo DOI is the preferred way to launch Binder links so that it will be stable far into the future.

### Default system: Preservation without Binder support

The preferred system for repository preservation on Zenodo is **not required** for your talk and repository to be preserved in the PyHEP Zenodo community collection.
The PyHEP workshop organizers will manually archive any talks that do not already have Zenodo DOIs into a community collection.
However, support for building Binder images from Zenodo DOIs is **only** available for projects that have been archived through the [Zenodo GitHub interface](https://zenodo.org/account/settings/github/).
If a project is manually archived, the built Binder image will launch into a Jupyter server with a `.zip` file of the Zenodo archive in it, instead of the unpacked archive.

## Installation

1. Install [Pixi](https://pixi.sh/latest/installation/)
2. Run

```
pixi install
```

or just

```
pixi run start
```
