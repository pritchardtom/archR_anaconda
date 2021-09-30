# Anaconda on SCW

This guide provides a brief overview of Anaconda, and how to use it on Hawk or Sunbird. For a more complete guide, please consult the official [Anaconda](https://docs.anaconda.com/) and [Conda](https://conda.io/projects/conda/en/latest/user-guide/index.html) documentation.

If you have any issues with Anaconda that are not covered in this guide, please login to [MySCW](https://scw.bangor.ac.uk/en/) and select the *Submit Support Ticket* option.  Provide as much information as you can, and one of the support team will provide assistance with your Anaconda problem.

## Table of Contents
 - [Introduction to Anaconda](#introduction-to-anaconda)
   - [What is Anaconda?](#what-is-anaconda)
   - [What is Conda?](#what-is-conda)
   - [When to use Anaconda](#when-to-use-anaconda)
 - [Using Anaconda on SCW](#using-anaconda-on-scw)
   - [Loading Anaconda](#loading-anaconda)
   - [Creating a New Conda Environment](#creating-a-new-conda-environment)

## Introduction to Anaconda

If you are already familiar with Anaconda, please skip to the

### What is Anaconda?

Anaconda is a distribution of Python, R, Conda, and a suite of 1500 packages focused on aiding scientific computing, and simplifying package management and virtual environments.

### What is Conda?

Conda is a package and virtual environment manager, which comes bundled with the Anaconda distribution.  Conda can manage packages and dependencies within any language, not just Python, and it is often equated with `yum` or `apt` as a result.

A conda environment is a directory that contains the specific collection of packages you have installed.  If you change one environment, your others are unaffected.

### When to use Anaconda

Anaconda, while useful to some, will not be required by all SCW users who require Python and other packages.  Where applicable, SCW users should try to make use of the existing software available on SCW before using Anaconda.

Here's a brief guide on how to select when to use Anaconda over other options:

| Scenario | Recommended Solution |
| -------- | -------------------- |
| Python version is installed but need Python packages not installed on SCW. | Use `pip -u` <package_name> or `virtualenv` if isolation required. |
| Python version is installed but need Python and non-Python packages not installed | Use Anaconda. |
| Python required is not installed, but still only need Python packages | Use Anaconda, or install Python manually in `$HOME` and use `pip`. |
| Python required not installed, but need Python and non-Python packages | Use Anaconda. |
| Require management of Python and non-Python languages/packages | Use Anaconda. |
| Require isolation to install Python packages | Use `pip` + `virtualenv/venv` or Anaconda. |

The above scenarios are Python-specific, but can also be applied to `R` and other languages/situations.

## Using Anaconda on SCW

These instructions should work on Hawk and Sunbird.

### Loading Anaconda

The following instructions will get Anaconda initialised on your SCW account:

```
module load anaconda/2021.05
source activate
```

If everything is successful, your Terminal prompt should now look like this:

```
(base) [s.a.user@sl1]$
```

**Please Note:** The version of Anaconda on Hawk/Sunbird might be updated more regularly than this documentation.  If in doubt as to which version is the latest on the system, please type `module load anaconda` on the login node and press the `TAB` key twice.  This should produce an output of all the available versions of Anaconda.  For example:

```
anaconda/2019.03  anaconda/2020.07  anaconda/2021.05  anaconda/3
```

**Please Note:** Users are unable to write to the `base` environment, so attempting a command like `conda install numpy` here will result in errors.  Users must create or activate an existing conda environment before continuing.


###Creating a New Conda Environment

Once you have loaded Anaconda, you can create a new conda environment with the following command:

```
conda create -n <name_of_env> <packages_to_install>
```
