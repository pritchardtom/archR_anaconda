# Anaconda on SCW

This guide provides a brief overview of Anaconda, and how to use it on Hawk or Sunbird. For a more complete guide, please consult the official [Anaconda](https://docs.anaconda.com/) and [Conda](https://conda.io/projects/conda/en/latest/user-guide/index.html) documentation.

If you have any issues with Anaconda that are not covered in this guide, please login to [MySCW](https://scw.bangor.ac.uk/en/) and select the *Submit Support Ticket* option.  Provide as much information as you can, and one of the support team will provide assistance with your Anaconda problem.

## What is Anaconda?

Anaconda is a distribution of Python, R, Conda, and a suite of 1500 packages focused on aiding scientific computing, and simplifying package management and virtual environments.

## What is Conda?

Conda is a package and virtual environment manager, which comes bundled with the Anaconda distribution.  Conda can manage packages and dependencies within any language, not just Python, and it is often equated with `yum` or `apt` as a result.

## When to use Anaconda

Anaconda, while useful to some, will not be required by all SCW users who require Python and other packages.  Where applicable, SCW users should try to make use of the existing software available on SCW before using Anaconda.

| Scenario | Recommended Solution |
| -------- | -------------------- |
| Python version is installed but need Python packages not installed on SCW. | Use `pip -u` <package_name> or `virtualenv` if isolation required. |
| Python version is installed but need Python and non-Python packages not installed | Use Anaconda. |
| Python required is not installed, but still only need Python packages | Use Anaconda, or install Python manually in `$HOME` and use `pip`. |
| Python required not installed, but need Python and non-Python packages | Use Anaconda. |
| Require management of Python and non-Python languages/packages | Use Anaconda. |
| Require isolation to install Python packages | Use `pip` + `virtualenv/venv` or Anaconda. |
