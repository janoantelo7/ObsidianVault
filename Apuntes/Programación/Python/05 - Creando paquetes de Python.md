---
source: https://packaging.python.org/en/latest/tutorials/packaging-projects/
tags:
  - clippings
  - python
---
# A simple project

This tutorial uses a simple project named `example_package_YOUR_USERNAME_HERE`. If your username is `me`, then the package would be `example_package_me`; this ensures that you have a unique package name that doesn’t conflict with packages uploaded by other people following this tutorial. We recommend following this tutorial as-is using this project, before packaging your own project.

Create the following file structure locally:

```bash
packaging_tutorial/
└── src/
    └── example_package_YOUR_USERNAME_HERE/
        ├── __init__.py
        └── example.py
```

The directory containing the Python files should match the project name. This simplifies the configuration and is more obvious to users who install the package.

Creating the file `__init__.py` is recommended because the existence of an `__init__.py` file allows users to import the directory as a regular package, even if (as is the case in this tutorial) `__init__.py` is empty.

`example.py` is an example of a module within the package that could contain the logic (functions, classes, constants, etc.) of your package. Open that file and enter the following content:

```python
def add_one(number):
    return number + 1
```

If you are unfamiliar with Python’s [modules](https://packaging.python.org/en/latest/glossary/#term-Module) and [import packages](https://packaging.python.org/en/latest/glossary/#term-Import-Package), take a few minutes to read over the [Python documentation for packages and modules](https://docs.python.org/3/tutorial/modules.html#packages).

Once you create this structure, you’ll want to run all of the commands in this tutorial within the `packaging_tutorial` directory.

## Creating the package files

You will now add files that are used to prepare the project for distribution. When you’re done, the project structure will look like this:

```bash
packaging_tutorial/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── example_package_YOUR_USERNAME_HERE/
│       ├── __init__.py
│       └── example.py
└── tests/
```

## Creating a test directory

`tests/` is a placeholder for test files. Leave it empty for now.

## Choosing a build backend

Tools like [pip](https://packaging.python.org/en/latest/key_projects/#pip) and [build](https://packaging.python.org/en/latest/key_projects/#build) do not actually convert your sources into a [distribution package](https://packaging.python.org/en/latest/glossary/#term-Distribution-Package) (like a wheel); that job is performed by a [build backend](https://packaging.python.org/en/latest/glossary/#term-Build-Backend). The build backend determines how your project will specify its configuration, including metadata (information about the project, for example, the name and tags that are displayed on PyPI) and input files. Build backends have different levels of functionality, such as whether they support building [extension modules](https://packaging.python.org/en/latest/glossary/#term-Extension-Module), and you should choose one that suits your needs and preferences.

You can choose from a number of backends; this tutorial uses [Hatchling](https://packaging.python.org/en/latest/key_projects/#hatch) by default, but it will work identically with [Setuptools](https://packaging.python.org/en/latest/key_projects/#setuptools),[Flit](https://packaging.python.org/en/latest/key_projects/#flit), [PDM](https://packaging.python.org/en/latest/key_projects/#pdm), and others that support the `[project]` table for .

> [!Note]
> Some build backends are part of larger tools that provide a command-line interface with additional features like project initialization and version management, as well as building, uploading, and installing packages. This tutorial uses single-purpose tools that work independently.

The `pyproject.toml` tells [build frontend](https://packaging.python.org/en/latest/glossary/#term-Build-Frontend) tools like [pip](https://packaging.python.org/en/latest/key_projects/#pip) and [build](https://packaging.python.org/en/latest/key_projects/#build) which backend to use for your project. Below are some examples for common build backends, but check your backend’s own documentation for more details.

```toml
[build-system]
requires = ["hatchling >= 1.26"]
build-backend = "hatchling.build"
```

The `requires` key is a list of packages that are needed to build your package. The [frontend](https://packaging.python.org/en/latest/glossary/#term-Build-Frontend) should install them automatically when building your package. Frontends usually run builds in isolated environments, so omitting dependencies here may cause build-time errors. This should always include your backend’s package, and might have other build-time dependencies. The minimum version specified in the above code block is the one that introduced support for [the new license metadata](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#license-and-license-files).

The `build-backend` key is the name of the Python object that frontends will use to perform the build.

Both of these values will be provided by the documentation for your build backend, or generated by its command line interface. There should be no need for you to customize these settings.

Additional configuration of the build tool will either be in a `tool` section of the `pyproject.toml`, or in a special file defined by the build tool. For example, when using `setuptools` as your build backend, additional configuration may be added to a `setup.py` or `setup.cfg` file, and specifying `setuptools.build_meta` in your build allows the tools to locate and use these automatically.
## Creating README.md
Open `README.md` and enter the following content. You can customize this if you’d like.

```md
# Example Package

This is a simple example package. You can use
[GitHub-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.
```
## Including other files
The files listed above will be included automatically in your [source distribution](https://packaging.python.org/en/latest/glossary/#term-Source-Distribution-or-sdist). If you want to include additional files, see the documentation for your build backend.
## Generating distribution archives
The next step is to generate [distribution packages](https://packaging.python.org/en/latest/glossary/#term-Distribution-Package) for the package. These are archives that are uploaded to the Python Package Index and can be installed by [pip](https://packaging.python.org/en/latest/key_projects/#pip).

Make sure you have the latest version of PyPA’s [build](https://packaging.python.org/en/latest/key_projects/#build) installed:

```bash
python3 -m pip install --upgrade build
```

```bash
py -m pip install --upgrade build
```

Now run this command from the same directory where `pyproject.toml` is located:
```bash
python3 -m build
```

```bash
py -m build
```

This command should output a lot of text and once completed should generate two files in the `dist` directory:

```bash
dist/
├── example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
└── example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz
```

The `tar.gz` file is a [source distribution](https://packaging.python.org/en/latest/glossary/#term-Source-Distribution-or-sdist) whereas the `.whl` file is a [built distribution](https://packaging.python.org/en/latest/glossary/#term-Built-Distribution). Newer [pip](https://packaging.python.org/en/latest/key_projects/#pip) versions preferentially install built distributions, but will fall back to source distributions if needed. You should always upload a source distribution and provide built distributions for the platforms your project is compatible with. In this case, our example package is compatible with Python on any platform so only one built distribution is needed.

## Installing your newly uploaded package

You can use [pip](https://packaging.python.org/en/latest/key_projects/#pip) to install your package and verify that it works. Create a [virtual environment](https://packaging.python.org/en/latest/tutorials/installing-packages/#creating-and-using-virtual-environments) and install your package from TestPyPI:

```bash
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-package-YOUR-USERNAME-HERE
```

```bash
py -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-package-YOUR-USERNAME-HERE
```

Make sure to specify your username in the package name!

pip should install the package from TestPyPI and the output should look something like this:

```bash
Collecting example-package-YOUR-USERNAME-HERE
  Downloading https://test-files.pythonhosted.org/packages/.../example_package_YOUR_USERNAME_HERE_0.0.1-py3-none-any.whl
Installing collected packages: example_package_YOUR_USERNAME_HERE
Successfully installed example_package_YOUR_USERNAME_HERE-0.0.1
```

Note

This example uses `--index-url` flag to specify TestPyPI instead of live PyPI. Additionally, it specifies `--no-deps`. Since TestPyPI doesn’t have the same packages as the live PyPI, it’s possible that attempting to install dependencies may fail or install something unexpected. While our example package doesn’t have any dependencies, it’s a good practice to avoid installing dependencies when using TestPyPI.

You can test that it was installed correctly by importing the package. Make sure you’re still in your virtual environment, then run Python:

```bash
python3
```

```bash
py
```

and import the package:

```bash
>>> from example_package_YOUR_USERNAME_HERE import example
>>> example.add_one(2)
3
```