---
layout: post
title: Publish your python package to pypi
---

## What is pypi
[pypi](https://pypi.org) (python package index) is byfar the most popular software repository for the python programming language. User can explore software packages developed and shared by the community across the world.
Use pypi to distribute your software across the globe. Its free to use, just sign-up and you can use a test and production sites for publishing your package.
Installation of the packages (distributed via pypi) are very easy and almost consistent across. Below command sounds familiar??
>pip install package-name

## Steps

- [Register to pypi](#pypi-account)
- [Prepare the files necessary for pypi](#pre-requisite)
- [Upload your package](#upload)
- [Install and validate](#validate)

---

## [Register to pypi](#pypi-account)

Goto [pypi](https://pypi.org) and [test.pypi]https://test.pypi.org/ and register with details like name, email and password. After registering and verifying email address, goto "API Tokens" section and add a token. Keep this token, which will be used for authentication while uploading your package to pypi via CLI.
**Note**: pypi and test.pypi are 2 different environments, later being test environment. Credentials aren't shared between 2 environments, registering and adding api tokens to be done twice.

## [Prepare the files necessary for pypi](#pre-requisite)
Create a folder with a unique memorable name that will be the package-name while uploading to pypi.
Create a folder as a repository and then Place/Create the following files in the structure as mentioned below:

**Folder**
```
- package-name
 - __init__.py
- app.py
- setup.py
- setup.cfg
- README.md
- License.txt
- requirements.txt
```

Let's see in details about the files that we added/created:
1) __init__.py --> Its required to import the directory as a package. This can be empty file.
2) app.py --> This is your python code. Classes/Modules that are generic enough and been felt by yourself that it will be useful be
3) setup.py
```
#**Content*
#Thissetup.py tells about your package. This is the build script for setuptools
import setuptools

with open("README.md", "r") as fh:
    long_description = fh.read()

setuptools.setup(
    name="package-name",
    version="0.1",
    author="author name",
    author_email="author email",
    description="Simple description",
    long_description=long_description,
    long_description_content_type="text/markdown",
    url="github url if used",
    packages=setuptools.find_packages(),
    data_files=[('', ['package-name/*.css'])],
    install_requires=['numpy>=1.19.1'],
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: License",
        "Operating System :: OS Independent",
    ],
    include_package_data=True,
    python_requires='>=3.6',
)
```
4) setup.cfg
```
#**Content**
[metadata]
description-file = README.md

```
5) README.md --> This is a markdown file, where you can provide description of the package. What its all about, features, how to use, how to install etc.
6) License.txt --> provide your package's license type and the limitations. For further details, pls check [here](https://choosealicense.com/).
7) requirements.txt --> provide details on external package dependencies that is applicable for running your code. Example below:
> numpy>=1.19.1

## [Upload your package](#upload)
Before getting ready to upload your package to test.pypi, install the following
> pip install twine
```
(twine is a utility for publishing python packages to pypi. Twine is one of the easiest and popular option available)
```
> pip install setuptools wheel
```
(Wheel helps in creating the wheel files that are appropriate build package format for pypi uploads)
(setuptools helps to install, build, download, upgrade and uninstall python packages)
```

We are all set now. Execute the following commands

> cd Folder
> python setup.py sdist bdist_wheel
> python -m twine upload --repository testpypi dist/*
```
(above command uploads your package to test.pypi.org)
(after executing the above command, many folders and files will be generated. For eg you can find .whl file & distribution zip file within dist folder, which is uploaded to pypi using twine below)
```
>python -m twine upload dist/*
```
Uploading distributions to https://upload.pypi.org/legacy/)
Enter your username: __token__
Enter your password: <enter the apikey that you stored while registering to pypi>
uploading.....
(above command uploads your package to pypi.org)
```

View your package at https://pypi.org/project/package-name

## [Install and validate](#validate)
Once your package is uploaded, you can install it in your local environment and validate
>pip install package-name

If there is any issue or updates are made to the file. Make the changes, update setup.py with new version and other necessary details and repeat the process from running > python setup.py sdist bdist_wheel
Feel free to reach out at my email to leave feedback and talk about the article.
