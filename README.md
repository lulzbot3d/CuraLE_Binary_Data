# CuraLE Binary Data

[![Conan Badge]][Conan]

[![Size Badge]][Size]
[![License Badge]][License]

Contains binary data for CuraLE releases, such as compiled translations and firmware.

## License

CuraLE Binary Data is released under terms of the AGPLv3 License. Terms of the license can be found in the LICENSE file or [on the GNU website.](http://www.gnu.org/licenses/agpl.html)

> In general, it boils down to:  
> **You need to share the source of any CuraLE Binary Data modifications if you make an application with CuraLE Binary Data.**

## System Requirements

### All Platforms

- Python 3.6 or higher

## How To Build

If you have never used [Conan](https://conan.io/) read their [documentation](https://docs.conan.io/en/latest/index.html)
which is quite extensive and well maintained. Conan is a Python program and can be installed using pip

### 1. Configure Conan

```bash
pip install conan --upgrade
conan config install https://github.com/lulzbot3d/Conan_LulzBot_Config.git
conan profile new default --detect --force
```

LulzBot developers need to request an account for our JFrog Artifactory server with IT

### 2. Clone CuraLE_Binary_Data

```bash
git clone https://github.com/lulzbot3d/CuraLE_Binary_Data.git
cd CuraLE_Binary_Data
```

## Creating a new CuraLE_Binary_Data Conan package

To create a new CuraLE_Binary_Data Conan package such that it can be used in CuraLE and UraniumLE, run the following command:

```shell
conan create . curale_binary_data/<version>@<username>/<channel> --build=missing --update
```

This package will be stored in the local Conan cache (`~/.conan/data` or `C:\Users\username\.conan\data` ) and can be used in downstream
projects, such as CuraLE and UraniumLE by adding it as a requirement in the `conanfile.py` or in `conandata.yml`.

Note: Make sure that the used `<version>` is present in the conandata.yml in the CuraLE_Binary_Data root

You can also specify the override at the commandline, to use the newly created package, when you execute the `conan install`
command in the root of the consuming project, with:

```shell
conan install . -build=missing --update --require-override=curale_binary_data/<version>@<username>/<channel>
```

## Developing CuraLE_Binary_Data In Editable Mode

You can use your local development repository downsteam by adding it as an editable mode package.
This means you can test this in a consuming project without creating a new package for this project every time.

```bash
    conan editable add . curale_binary_data/<version>@<username>/<channel>
```

Then in your downsteam projects root directory (such as CuraLE), override the package with your editable mode package.

```shell
conan install . -build=missing --update --require-override=curale_binary_data/<version>@<username>/<channel>
```

<!---------------------------------------------------------------------------------------------------------------->

[Conan Badge]: https://img.shields.io/github/actions/workflow/status/lulzbot3d/CuraLE_Binary_Data/conan-package.yml?style=for-the-badge&logoColor=white&logo=Conan&label=Conan%20Package
[Size Badge]: https://img.shields.io/github/repo-size/lulzbot3d/CuraLE_Binary_Data?style=for-the-badge&logoColor=white&logo=GoogleAnalytics
[License Badge]: https://img.shields.io/github/license/lulzbot3d/CuraLE_Binary_Data?style=for-the-badge&logoColor=white&logo=GNU

[Conan]: https://github.com/lulzbot3d/CuraLE_Binary_Data/actions/workflows/conan-package.yml
[Size]: https://github.com/lulzbot3d/CuraLE_Binary_Data
[License]: LICENSE