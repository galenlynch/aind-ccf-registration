# aind-ccf-registration

[![License](https://img.shields.io/badge/license-MIT-brightgreen)](LICENSE)
![Code Style](https://img.shields.io/badge/code%20style-black-black)

Source code to register SmartSPIM datasets to the CCF Allen Atlas.

This module is part of a pipeline. Therefore, it assumes that the
fused image comes in OME-Zarr format with different multiscales.
At this point, we are using ANTS for the image registration and it's
not possible to use the original resolution of the data. In consequence,
we are using the 3rd multiscale from the original resolution.

$$resX=origResX*(2^m)$$
$$resY=origResY*(2^m)$$
$$resZ=origResZ*(2^m)$$

Where $$m$$ is the provided multiscale. By default, we are using the 3rd. Afterwards, we resample the image to match the $$25um$$ microns space and then, we register the resulting image to the Allen CCF atlas.

## Installation
To use the software, in the root directory, run
```
pip install -e .
```

To develop the code, run
```
pip install -e .[dev]
```

In Code Ocean, it is necessary to create 5 text parameters:
1. input_data: This parameter

## Contributing

### Linters and testing

There are several libraries used to run linters, check documentation, and run tests.

- Please test your changes using the **coverage** library, which will run the tests and log a coverage report:

```
coverage run -m unittest discover && coverage report
```

- Use **interrogate** to check that modules, methods, etc. have been documented thoroughly:

```
interrogate .
```

- Use **flake8** to check that code is up to standards (no unused imports, etc.):
```
flake8 .
```

- Use **black** to automatically format the code into PEP standards:
```
black .
```

- Use **isort** to automatically sort import statements:
```
isort .
```

### Pull requests

For internal members, please create a branch. For external members, please fork the repo and open a pull request from the fork. We'll primarily use [Angular](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit) style for commit messages. Roughly, they should follow the pattern:
```
<type>(<scope>): <short summary>
```

where scope (optional) describes the packages affected by the code changes and type (mandatory) is one of:

- **build**: Changes that affect the build system or external dependencies (example scopes: pyproject.toml, setup.py)
- **ci**: Changes to our CI configuration files and scripts (examples: .github/workflows/ci.yml)
- **docs**: Documentation only changes
- **feat**: A new feature
- **fix**: A bug fix
- **perf**: A code change that improves performance
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **test**: Adding missing tests or correcting existing tests

### Documentation
To generate the rst files source files for documentation, run
```
sphinx-apidoc -o doc_template/source/ code
```
Then to create the documentation html files, run
```
sphinx-build -b html doc_template/source/ doc_template/build/html
```
More info on sphinx installation can be found here: https://www.sphinx-doc.org/en/master/usage/installation.html
