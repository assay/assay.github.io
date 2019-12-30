---
layout: post
title: "Bazel + Python: folder structure example"
feature-img: assets/img/unsplash/code-grey.jpeg
tags: [Bazel, Python]
author-id: nettle
---

[Bazel](https://bazel.build/) build system can be used to manage Python code.
It is convenient to have one build system for many different languages which is common for large projects.
In addition Bazel provides at least two more advantages:
it can run and cache tests and it does not pollute the code with **pyc** files.

[This simple example](https://github.com/nettle/bazel-python-unittest) demonstrates a possible way
to organize **python code + unittest + bazel** in a convenient folder structure.

Bazel BUILD targets
-------------------

We normally use Bazel rules [py_binary](https://docs.bazel.build/be/python.html#py_binary)
and [py_library](https://docs.bazel.build/be/python.html#py_library) for Python targets.

Example for our case:
```python
py_binary(
    name = "sample",
    srcs = ["sample.py"],
)
```

Bazel test targets for python are defined using [py_test](https://docs.bazel.build/be/python.html#py_test) rule.
```python
py_test(
    name = "test_one",
    srcs = ["test/test_one.py"],
    deps = ["sample"],
)

py_test(
    name = "test_two",
    srcs = ["test/test_two.py"],
    deps = ["sample"],
)

py_test(
    name = "test_three",
    srcs = ["test/test_three.py"],
    deps = ["sample"],
)
```

Tests can be also grouped in suites by [test_suite](https://docs.bazel.build/be/general.html#test_suite) rule.
```python
test_suite(
    name = "all_tests",
    tests = [
        "test_one",
        "test_two",
        "test_three",
    ],
)
```

With targets defined like above we can use `bazel run` and `bazel test` commands to execute python code and unit tests.

### Advantages:

* Source code is separated from tests
* Folder is "clean" from *.pyc files (when using Bazel)
* Can run both Bazel test and Python unittest

Files:
------

```tree
├── sample.py              - Sample python module
├── BUILD                  - Bazel build file
├── WORKSPACE              - Bazel workspace file
└── test                   - Folder for unittests
     ├── test/run.py       - Test launcher
     └── test/test_*.py    - Unit tests
```

How to build?
-------------
Build all using Bazel

    bazel build :*


How to run?
-----------
Run sample module using Bazel:

    bazel run :sample


How to test?
------------
Run all Bazel tests:

    bazel test :*

or run Bazel test suite:

    bazel test :all_tests


How to debugging tests?
-----------------------
You can also run all or particular tests using run_tests (test/run.py) launcher:

    bazel run :run_tests

See options:

    bazel run :run_tests -- -h

Increase verbosity:

    bazel run :run_tests -- -vv

Run particular test case:

    bazel run :run_tests -- test_one.TestOne

or particular test function:

    bazel run :run_tests -- test_one.TestOne.test_one

Run test function with debug logs:

    bazel run :run_tests -- test_one.TestOne.test_one -vvv


You can also run unit tests directly without Bazel with the same options:

    python test/run.py

Note on test launcher
---------------------

You have probably noticed python file [test/run.py](https://github.com/nettle/bazel-python-unittest/blob/master/test/run.py)
which is in fact optional and provides the possibility to run unittests in normal Python environment.
It is just a wrapper script which parses arguments (using **argparse**), load tests (**unittest.TestLoader**)
and finally calls **unittest.TextTestRunner**.

Note that the following command can be used instead of that script:

    python -B -m unittest discover -s test
