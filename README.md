# PyHEP Notebook Talk Example

Example repository structure for a PyHEP style "notebook talk"

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)
[![DOI](https://zenodo.org/badge/381276327.svg)](https://zenodo.org/badge/latestdoi/381276327)

> N.B.: If you have questions on how to build a notebook talk, or the instructions below for sharing your notebook talk with Binder and preserving it with Zenodo please ask in the [GitHub Discussions](https://github.com/matthewfeickert/pyhep-notebook-talk-example/discussions)!

## Presentation Resources

> **PyHEP 2023 Update:** PyHEP 2023 will be using a BinderHub that has been deployed by IRIS-HEP's [Scalable Systems Laboratory](https://iris-hep.org/ssl.html) (SSL) at https://binderhub.ssl-hep.org/ which requires authentication with CILogon.
> The instructions are the same as from previous years, with the exception of all urls that use `mybinder.org` will now use `binderhub.ssl-hep.org`.
> A walkthrough video of the workflow is also [available on the HSF YouTube channel](https://youtu.be/4D6eYHNQip0).
>
> **N.B.:** The CILogon identity providers that will work for the SSL BinderHub are verified institutions with signed agreements.
> This means that CERN and any university will work, but Google and GitHub will not.
> If you do not have an affiliation with a verified institution you won't be able to use the SSL BinderHub but you can follow along on the public mybinder BinderHub at http://mybinder.org/.

Before getting into the specifics of how to setup a repository to make it runnable with Binder and preservable with Zenodo, it is a good idea to first think about how to give a talk with a Jupyter notebook.
[Jim Pivarski](https://github.com/jpivarski) has a very good June 2021 PyHEP Topical meeting talk all about things to think about and consider when giving a talk with a Jupyter notebook: [How to give a good Jupyter talk](https://indico.cern.ch/event/1044648/).

## Interactivity with Binder

### Minimum Required Setup

The minimum setup required is simply a repository with the Jupyter notebook that you'll be using and the `requirements.txt` or environment config file that is used to specify and install all of your code's dependencies.
Note that it is rather important to **exactly** specify the requirements with `==` to avoid the repository code breaking in the future.

### Recommended Setup

Ideally, in addition to the minimum requirements, you'll also make the repository runnable on [Binder](https://mybinder.org/).
The easiest way to do this is to simply ensure that _all_ of your dependencies are properly specified in your `requirements.txt` file and then to create a `binder` directory in the top level of the repository and place the `requirements.txt` file in it.
Binder knows to look for configuration files under the `binder` directory so you can put all of your [Binder configuration files](https://mybinder.readthedocs.io/en/latest/using/config_files.html) there.
Additionally, specifying the version of Python that should be used to run the code in a [`runtime.txt` file](https://mybinder.readthedocs.io/en/latest/using/config_files.html#runtime-txt-specifying-runtimes) under the `binder` directory is useful.

Once these requirements have been met and commit to your repository if you visit [binderhub.ssl-hep.org](https://binderhub.ssl-hep.org/) and paste the URL of your GitHub repository (or Zenodo DOI!) into the text box, Binder will generate a badge for your repository README.
If a user just clicks that badge, the Binder build will run if there already isn't a built image for it and then launch the user into an interactive session inside of the image running on Binder Federation resources.

Below is an example of a URL that will launch the `talk.ipynb` notebook in this repository into a JupyterLab environment.

```
https://binderhub.ssl-hep.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb
```

and its badge

[![Binder](https://mybinder.org/badge_logo.svg)](https://binderhub.ssl-hep.org/v2/gh/matthewfeickert/pyhep-notebook-talk-example/HEAD?urlpath=lab/tree/talk.ipynb)

#### Jupyter Lab Optional Launcher

If you'd like to have your Binder badge [launch into a JupyterLab environment](https://mybinder.readthedocs.io/en/latest/howto/user_interface.html#jupyterlab) instead of Jupyter Notebook have the URL end with `?urlpath=lab/tree/path-to-the-notebook-you-want.ipynb`.

## Zenodo DOIs

### Recommended System: Preservation with Binder support

To preserve the repository with your talk as best as possible, have [Zenodo](https://zenodo.org/) build a Zenodo archive and mint a DOI for your repository.
To do this:

1. Create an account on [zenodo.org](https://zenodo.org/).
2. [Follow the instructions](https://zenodo.org/account/settings/github/) on syncing GitHub repositories that you control with Zenodo.
3. Create a new GitHub release (e.g. "pyhep-2023) to trigger an archive capture.
4. Add the minted DOI to your repository as a badge.

This DOI can then be used by the PyHEP workshop organizers to add your Zenodo archive to the relevant PyHEP community collection on Zenodo. c.f. [PyHEP 2023's Zenodo community](https://zenodo.org/communities/pyhep2023) as an example.

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

In a clean virtual environment install the dependencies (which are under the `binder` directory)

```console
python -m pip install -r binder/requirements.txt
```
