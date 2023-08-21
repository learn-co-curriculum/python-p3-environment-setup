# Environment Setup

## Learning Goals

- Use pyenv to use different Python versions
- Set up virtual environment using pipenv

---

## Key Vocab

- **Module**: a file containing Python definitions and statements. A module's
  functions, classes, and global variables can be accessed by other modules.
- **Package**: a collection of modules that can be accessed as a group using the
  package name.
- **`import`**: the Python keyword used to access data from other packages and
  modules inside of the current module.
- **PyPI**: the **Py**thon **P**ackage **I**ndex. A repository of Python
  packages that can be downloaded and made available to your application.
- **`pip`**: the command line tool used to download packages from PyPI. `pip` is
  installed on your computer automatically when you download Python.
- **Virtual Environment**: a collection of modules, packages, and scripts that
  can be activated or deactivated at any time.
- **Pipenv**: a virtual environment tool that uses `pip` to manage the modules,
  packages, and scripts that you intend to use in your application.

---

## Introduction

In this lesson we will talk about environment tools like pyenv and pipenv. These
tools allows us to separate different Python environments for all kinds of use
cases. This is useful when we need an isolated environment with libraries and
specific versions of Python.

---

## Pyenv

In an earlier lesson, you installed pyenv and Python 3.8.13. (If needed, you can
use the following instructions to install pyenv for your operating system.)

[pyenv install instructions](https://github.com/pyenv/pyenv#installation)

Run the following command to confirm pyenv was installed for version 3.8.13:

```console
$ pyenv versions
  system
* 3.8.13 (set by /Users/username/.pyenv/version)
  ...
```

We can see the different versions of Python available to install using the
following command

```console
$ pyenv install -l
Available versions:
  2.1.3
  2.2.3
  2.3.7
  ...
  ...
```

Lets install a new version of Python (3.11). We can do this using the following
command

```console
$ pyenv install 3.11
```

To set the global Python version to the new version 3.11:

```console
$ pyenv global 3.11
```

Confirm the current global Python version (full version 3.11.x may differ):

```console
$ python3 --version
Python 3.11.4
```

Now we can run Python code with version 3.11.x.

Let's set the global Python version back to 3.8.13:

```console
$ pyenv global 3.8.13
```

Confirm the global Python version:

```console
$ python3 --version
Python 3.8.13
```

---

## Pipenv

Pyenv allows us to manage the version of Python we are working with.

What if we want to manage dependencies as well?

Pipenv automatically creates and manages a virtualenv for your projects, it also
adds/removes packages from your Pipfile as you install/uninstall packages

To install pipenv follow the instructions here
[pipenv install](https://pipenv.pypa.io/en/latest/installation/)

To create a virtual environment using pipenv we can use the following command.

```bash
pipenv --python 3.11
```

In the Python flag we can define which version of `--python` we want to use.

You will notice a `Pipfile` and a `Pipfile.lock` have been added to the
directory.

The `Pipfile` describes the dependencies we have installed and the Python
version.

```text
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]

[dev-packages]

[requires]
python_version = "3.11"
python_full_version = "3.11.4"

```

The `Pipfile.lock` describes all the dependencies our dependencies rely on. The
lock file gives us the ability to produce a deterministic and reproducible
project environment.

We can now install a library into the virtual environment. Lets use the
`requests` library as an example

```console
$ pipenv install requests
```

if we want to install a specific version of the requests library we can pin the
version in the command

```console
$ pipenv install requests==2.28.1
```

Pipenv has created a virtual environment for our project. We can see the
location of this virtual environment by using the command (your location will
differ):

```console
$ pipenv --venv
Successfully created virtual environment!
Virtualenv location: /Users/username/python-p3-environment-setup/.venv
```

Pipenv allows us to install dev dependencies. We can do so by adding the `--dev`
argument.

```bash
pipenv install pytest --dev
```

Pytest will be added to the Pipfile as a dev dependency

Dev dependencies are modules which are not needed in production but they help us
develop and test the code.

How do we get into our virtual environment?

Using the following command we can use the virtual environment and run commands
inside of it.

```bash
pipenv shell
```

Now we are in the virtual environment and have access to the dependencies we
defined in the Pipfile. If we run the following commands in the virtual
environment we will see that we can import the `requests` module we installed
previously using `pipenv install requests`.

```console
$ python
>>> import requests
>>> exit()
```

If you ever need to remove a virtual environment you can use the `pipenv --rm`
command.

```console
$ pipenv --rm
Removing virtualenv (/Users/username/python-p3-environment-setup/.venv)...
```

This command can help you debug any conflicting environment issues. After
running the remove command you can run `pipenv install` again to create a new
virtual environment.

Now we can write all our code in this directory and run it in the deterministic
virtual environment. If we have a Python file called `program.py` we can use the
following command to run it in the virtual environment.

```console
$ pipenv run python program.py
```

---

Let's confirm you are no longer in a virtual environment and that your Python
version is 3.8.13:

```console
$ pipenv --rm
Removing virtualenv (/Users/username/python-p3-environment-setup/.venv)...
```

```console
$ python3 --version
```

## Conclusion

Virtual environments allow us to have a deterministic and predictable runtime
for our Python projects. We can define specific versions for Python and the
dependencies we need. We can easily add new virtual environments for multiple
projects we have on our machine.

---

## Resources

- [Python 3 Documentation](https://docs.python.org/3/)
- [Pyenv](https://github.com/pyenv/pyenv/)
- [Pipenv](https://pipenv.pypa.io/en/latest/)
