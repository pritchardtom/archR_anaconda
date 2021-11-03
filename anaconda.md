# Anaconda on SCW

This guide provides a brief overview of Anaconda, and how to use it on Hawk or Sunbird. For a more complete guide, please consult the official [Anaconda](https://docs.anaconda.com/) and [Conda](https://conda.io/projects/conda/en/latest/user-guide/index.html) documentation.

If you have any issues with Anaconda that are not covered in this guide, please submit a [Support Ticket](https://portal.supercomputing.wales/index.php/index/submit-support-ticket/), and one of the team will provide assistance.

## Table of Contents
 - [Introduction to Anaconda](#introduction-to-anaconda)
   - [What is Anaconda?](#what-is-anaconda)
   - [What is Conda?](#what-is-conda)
 - [Using Anaconda on SCW](#using-anaconda-on-scw)
   - [Loading Anaconda](#loading-anaconda)
   - [Creating a New Conda Environment](#creating-a-new-conda-environment)
     - [Example: Creating a TensorFlow CPU Environment](#example-creating-a-tensorflow-cpu-environment)
   - [Loading an Existing Conda Environment](#loading-an-existing-conda-environment)
     - [Example: Loading The TensorFlow CPU Environment](#example-loading-the-tensorflow-cpu-environment)
   - [Leaving a Conda Environment](#leaving-a-conda-environment)
  - [Managing Conda Packages and Environments](#managing-conda-packages-and-environments)
    - [Common Commands](#common-commands)
    - [Using pip and Other Package Managers](#using-pip-and-other-package-managers)
      - [Example: Using pip to install TensorFlow](#example-using-pip-to-install-tensorflow)
      - [No need for pip install user](#no-need-for-pip-install-user)
  - [Common Issues and Troubleshooting](#common-issues-and-troubleshooting)
    - [Disk and File Space Errors ](#disk-and-file-space-errors)
      - [Potential Solutions](#potential-solutions)
    - [Permission Errors](#permission-errors)
      - [Potential Solutions](#potential-solutions)
    - [Package Not Found Error](#package-not-found-error)
      - [Potential Solutions](#potential-solutions)
    - [Conda Channels](#conda-channels)

## Introduction to Anaconda

If you are already familiar with Anaconda, please skip to the [Using Anaconda on SCW](#using-anaconda-on-scw) section.

### What is Anaconda?

Anaconda is a distribution of Python, R, Conda, and a suite of 1500 packages focused on aiding scientific computing, and simplifying package management and virtual environments.

### What is Conda?

Conda is a package and virtual environment manager, which comes bundled with the Anaconda distribution.  Conda can manage packages and dependencies within any language, not just Python, and it is often equated with `yum` or `apt` as a result.

A conda environment is a directory that contains the specific collection of packages you have installed.  If you change one environment, your others are unaffected.

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

### Creating a New Conda Environment

Once you have loaded Anaconda, you can create a new conda environment with the following command:

```
conda create -n <name_of_env> <packages_to_install>
```

Where:

- `<name_of_env>` is the name you'd like to give your conda env; and,
- `<packages_to_install>` are a list of conda packages you want installed into this new conda environment.

**Please Note:** Conda environments will be installed under: `/home/$USER/.conda/`.

**Please Note:** It is advisable to run the `myquota` command from your SCW Terminal prior to creating a conda environment/installing packages, and ensure you have enough disk/file capacity.  See the {\bf Common Issues} section for more information.

Once all the packages/dependencies have installed you need to activate your new conda environment in order to use it:

```
conda activate <name_of_env>
```

If everything worked correctly, your Terminal should now reflect this activation by looking similar to:

```
(<name_of_env>) [s.a.user@sl1]$
```

**Please Note:** It is good practice to run the following command once your conda environment is set up correctly:

```
conda clean -a
```

This will remove all unused packages/tarballs/files, and will help reduce any potential issues with users exceeding file/disk usage quotas.

We will now use these commands to create a TensorFlow (CPU version) conda environment.

#### Example: Creating a TensorFlow (CPU) Environment

We will make use of the above commands to create a new conda environment called `tenflow`, which will install:

- Python 3.8;
- TensorFlow;
- Pandas; and
- Keras

```
#if not already done:
module load anaconda/2021.05
source activate

#create new conda environment (accept prompt & wait for packages/dependencies to download & install):
conda create -n tenflow python=3.8 tensorflow pandas keras

#activate new conda env:
conda activate tenflow

#Terminal prompt should now look like this:
(tenflow) [s.a.user@sl1]$

#clean up install (accept prompt & wait for process to end):
conda clean -a
```

You are now ready to use TensorFlow within your new conda environment.

**Please Note:** You can specify specific package versions, as we did in the example above for Python, or allow conda to get the default versions that are compatible with all the packages and dependencies.  

### Loading an Existing Conda Environment

If you already have a conda environment you wish to load, there is no need to use the `conda create` command used above.  Instead, the following should be executed:

```
#use this to get a list of your conda envs (optional)
#useful if forgotten name of your conda env(s):
conda info -e

#activate the conda environment of your choice:
conda activate <env_name>

#Terminal prompt should now look like this:
(<env_name>) [s.a.user@sl1]$
```

#### Example: Loading The TensorFlow CPU Environment

We will now load the TensorFlow environment we created earlier `tenflow`.  This example assumes the user has already loaded the Anaconda module and run the `source activate` command.

```
#already know the conda env name, so:
conda activate tenflow

#Terminal prompt should now look like this:
(tenflow) [s.a.user@sl1]$
```

You are now ready to use your TensorFlow conda environment.

### Leaving a Conda Environment

To leave a conda environment, simply execute the following command:

```
(tenflow) [s.a.user@sl1]$ conda deactivate
(base) [s.a.user@sl1]$ conda deactivate
[s.a.user@sl1]$
```

Anaconda keeps track of all the environments you've activated, and will cycle back through them with each `conda deactivate` you execute.  For example:

```
#we start in base by default:
(base) [s.a.user@sl1]$

#we load first environment:
conda activate my_env1
(my_env1) [s.a.user@sl1]$

#we load second environment:
conda activate my_env2
(my_env2) [s.a.user@sl1]$

#when we run conda deactivate, we return to my_env1:
conda deactivate
(my_env1) [s.a.user@sl1]$

#running conda deactivate for a second time:
#returns us to base:
conda deactivate
(base) [s.a.user@sl1]$
```

## Managing Conda Packages and Environments

Below are some common commands to assist in the management of conda packages and environments.

### Common Commands
| Command | Description |
| ------- | ----------- |
| conda list | lists all installed pkgs in conda |
| conda list -n <env_name> | lists all installed pkgs in <env_name> |
| conda list -n <env_name> <pkg> | check if <pkg> installed in <env_name> |
| conda search <pkg> | search for <pkg> |
| conda install <pkg> | install <pkg> |
| conda install <pkg=ver> | install specific ver of <pkg> |
| conda update <pkg> | updates <pkg> |
| conda remove <pkg> | remove <pkg> from current env |
| conda remove <pkg1 pkg2...> | remove multiple pkgs from current env |
| conda remove -n <env_name> <pkg> | remove pkgs from specific env |
| conda remove -n <env_name> --all | remove/delete conda env <env_name> |
| conda -V | returns version of Conda |
| conda info | returns summary of Conda install |
| conda info -e | lists all your conda envs |
| conda create <env_name> <pkgs> | create conda env/install pkgs |
| conda activate <env_name> | activate <env_name> |
| conda deactivate | exits current conda env |

### Using pip and Other Package Managers

Some software packages are not available as conda recipes.  However, we can still use conda environments to create a sandbox for the various software you require, and use pip or other package managers to install them in this environment.

#### Example: Using pip to install TensorFlow

Whilst TensorFlow is available as a conda recipe, there is often a delay in the latest releases appearing in conda, so in this example we will use pip to install TensorFlow to a new conda environment:

```
module load anaconda/2021.05
source activate

conda create -n pip_test python=3.8
conda activate pip_test
pip install tensorflow
```

#### No need for pip install user

When typically using pip on SCW, users have to provide the `--user` flag to install packages in their `$HOME/.local` directory.  This is because, by default, pip will install packages to a location users do not have write permissions.

However, when inside a conda environment with pip installed, the default install location for packages is `$HOME/.conda`, which you already have permission to write to, so there is no need to provide `--user`.


## Common Issues and Troubleshooting

Here are some of the common issues users experience when using Anaconda.  If you are experiencing a problem not listed here and require assistance, please login to [MySCW](https://scw.bangor.ac.uk/en/) and submit a Support Ticket.

### Disk and File Space Errors

It is advisable to run `myquota` prior to creating a new conda environment to ensure you have enough space.  However, if you experience errors regarding disk or file space limits, execute the `myquota` command from your SCW Terminal and check:

- That your Filesystem *space* is not close to the *limit*; and,
- That the number of *files* in your `$HOME` is not close to its *limit*.

#### Potential Solutions

- Free-up disk and/or file usage by:
  - Deleting/transferring unused files from you `$HOME` directory.
  - Run `conda info -e` and delete any conda environments no longer needed.
  - Use `conda clean -a` command to remove superfluous conda files downloaded during installation of environments.

If none of the above solutions are practical, or do not free-up enough space/files to create and install your conda environment, please request a temporary extension to your quota limits.

**Please Note:** Please do not install conda environments in your `/scratch/$USER` directory.

### Permission Errors

If you experience permission errors during the installation/update/deletion of a new environment or package.

#### Potential Solutions

- Check you are not in the `base` environment when trying to install conda or pip packages.

**Please Note:**  It's fine to use `conda create` when in `base` to create new environments.

### Package Not Found Error

When attempting to install packages to your conda environment, you receive a `PackageNotFoundError` error, or something similarly worded.

#### Potential Solutions

- Double check the obvious: no typos/errors in package name or version.
- Check documentation for package installation instructions.
- Use `conda search <pkg_name>` to ensure package exists in conda.
- It could be the *Channels* (see below).

#### Conda Channels

When you instruct conda to install a package, it will search certain channels for that package name and version (if provided by user).  These default channels can be seen by executing `conda info`.  Examples of such channels include:

```
repo.anaconda.com/pkgs/main/linux-64
repo.anaconda.com/pkgs/main/noarch
conda.anaconda.org/conda-forge/linux-64
conda.anaconda.org/conda-forge/noarch
conda.anaconda.org/intel/linux-64
conda.anaconda.org/intel/noarch
```

If you have checked the obvious, and are still having issues, it is likely that the package you are attempting to install cannot be found in these default channels.  This will usually be clear by the package installation instructions containing the `--channel`  `-c` flag as part of the command.

Here's a quick example to illustrate this:

```
conda activate my_env
conda install survos  #Returns PackagesNotFoundError

#Why? Because survos is in the ccpi channel, which is not a default channel conda searches. This will work:
conda install -c ccpi survos

#template is:
conda install -c <channel_name> <pkg_name>
```

To learn more about Channels, please consult the [offical documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html).
