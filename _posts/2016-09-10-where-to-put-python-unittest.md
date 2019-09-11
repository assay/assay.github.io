---
layout: post
title: "Where to put Python unittest?"
feature-img: assets/img/pexels/python.jpg
tags: [Python]
author-id: nettle
---

Somewhat convenient folder structure for Python unit tests.

************************

## Simple package

Let's say we need a simple Python package which implements some functionality
and supposed to be a part of something bigger.
It must be also very simple to use from other packages,
just like `import my_package`.

When we start developing our Python package it usually looks like the following:

```tree
my_package
├── __init__.py
├── one_class.py
└── another_class.py

```

## Adding unit tests

After some time, the sooner the better, we add unit tests,
which tend to hide among functional files.
So we mix implementation and test files, like this:

```tree
my_package
├── __init__.py
├── one_class.py
├── another_class.py
├── test_one_class.py
└── test_another_class.py

```

We typically write tests using [unittest](https://docs.python.org/library/unittest) library.
In tests we do `import one_class` etc to load implementation modules.
So `test_one_class.py` may look like:

```python
"""
Typical test cases for one_class module
"""
import unittest

import one_class


class TestOneClass(unittest.TestCase):
    """Unittest class for one_class module"""

    def test_one_class(self):
        """Test one_class"""
        self.assertTrue(one_class.One.something)


if __name__ == "__main__":
    unittest.main()
```

From `my_package` unit tests can be executed using the following command:

```shell
python -m unittest discover
```

## Moving to `test` folder

Someone likes this mix of implementation and tests, but not me.
I prefer test files to be separated from module implementation.
At the same time, test files should belong to the module and should be located
in a special folder called `test`, like this:

```tree
my_package
├── __init__.py
├── one_class.py
├── another_class.py
└── test
    ├── test_one_class.py
    └── test_another_class.py

```

Tests still can be ran from `my_package` folder,
however we should define start directory using `--start-directory` or just `-s`:

```shell
python -m unittest discover -s test
```

## How to run tests from `test` folder?

The only problem may happen if you would like to run tests from `test` directory.
Unfortunately in Python we cannot import modules from upper level.
But this can be solved with the following function:

```python
import imp
import os


def load_upper_module(file_name):
    """Load module from upper directory (..) by file name"""
    module_path = os.path.abspath(
        os.path.join(os.path.dirname(__file__), os.pardir, file_name))
    return imp.load_source(file_name, module_path)
```

This function takes Python module file name, e.g. `one_class.py` in our case.

It can be called from `setUpClass` class method of `unittest.TestCase`
to load module to `cls.module_under_test` every time when TestCase is loaded.
The following helper class shows how to do that:

```python
class TestCase(unittest.TestCase):
    """TestCase class which loads module_file_name as a module under test"""

    @classmethod
    def setUpClass(cls):
        """Load module"""
        cls.module_under_test = load_upper_module(cls.module_file_name)
```

We can put both `load_upper_module` and helper `TestCase` class
into, e.g. `utils` module.

Then use it like this:

```python
"""
Test cases for one_class module

Module utils implements TestCase helper class
which loads module from upper directory
"""
import unittest

import utils


class TestOneClass(utils.TestCase):
    """Unittest class for one_class module"""
    module_file_name = "one_class.py"

    def test_one_class(self):
        """Test one_class"""
        self.assertTrue(self.module_under_test.One.something)


if __name__ == "__main__":
    unittest.main()
```

Now we can run tests from `test` and from `my_package` folders.

Find sample code [here](https://github.com/nettle/python-simple-test).
