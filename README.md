# CuraLEBinaryData

[![Conan Package](https://img.shields.io/github/actions/workflow/status/lulzbot3d/CuraLEBinaryData/conan-package.yml?style=for-the-badge&color=4c6987&logo=Conan&label=Conan%20Package)](https://github.com/lulzbot3d/CuraLEBinaryData/actions/workflows/conan-package.yml)

[![Repo Size](https://img.shields.io/github/repo-size/lulzbot3d/CuraLEBinaryData?style=for-the-badge&logoColor=white&color=446a30&logo=GoogleAnalytics)](https://github.com/lulzbot3d/CuraLEBinaryData)
[![License](https://img.shields.io/badge/License-AGPLv3-336887.svg?style=for-the-badge&logo=GNU)](LICENSE)

Contains binary data for CuraLE releases, such as compiled translations and firmware.

## License

CuraLEBinaryData is released under terms of the AGPLv3 License. Terms of the license can be found in the LICENSE file or [on the GNU website.](http://www.gnu.org/licenses/agpl.html)

> In general, it boils down to:  
> **You need to share the source of any CuraLEBinaryData modifications if you make an application with CuraLEBinaryData.**

## System Requirements

### All Platforms

- Python 3.6 or higher

## How To Build

> **Note:**  
> We are currently in the process of switch our builds and pipelines to an approach which uses [Conan](https://conan.io/) and pip to manage our dependencies, which are stored on our JFrog Artifactory server and in the pypi.org. At the moment not everything is fully ported yet, so bare with us.

If you have never used [Conan](https://conan.io/) read their [documentation](https://docs.conan.io/en/latest/index.html)
which is quite extensive and well maintained. Conan is a Python program and can be installed using pip

### 1. Configure Conan

```bash
pip install conan --upgrade
conan config install https://github.com/lulzbot3d/conan-config-le.git
conan profile new default --detect --force
```

Community developers would have to remove the Conan cura-le repository because it requires credentials.

LulzBot developers need to request an account for our JFrog Artifactory server with IT

```bash
conan remote remove cura-le
```

### 2. Clone CuraLEBinaryData

```bash
git clone https://github.com/lulzbot3d/CuraLEBinaryData.git
cd CuraLEBinaryData
```

## Creating a new CuraLEBinaryData Conan package

To create a new CuraLEBinaryData Conan package such that it can be used in CuraLE and UraniumLE, run the following command:

```shell
conan create . curalebinarydata/<version>@<username>/<channel> --build=missing --update
```

This package will be stored in the local Conan cache (`~/.conan/data` or `C:\Users\username\.conan\data` ) and can be used in downstream
projects, such as CuraLE and UraniumLE by adding it as a requirement in the `conanfile.py` or in `conandata.yml`.

Note: Make sure that the used `<version>` is present in the conandata.yml in the CuraLEBinaryData root

You can also specify the override at the commandline, to use the newly created package, when you execute the `conan install`
command in the root of the consuming project, with:

```shell
conan install . -build=missing --update --require-override=curalebinarydata/<version>@<username>/<channel>
```

## Developing CuraLEBinaryData In Editable Mode

You can use your local development repository downsteam by adding it as an editable mode package.
This means you can test this in a consuming project without creating a new package for this project every time.

```bash
    conan editable add . curalebinarydata/<version>@<username>/<channel>
```

Then in your downsteam projects root directory (such as CuraLE), override the package with your editable mode package.

```shell
conan install . -build=missing --update --require-override=curalebinarydata/<version>@<username>/<channel>
```
