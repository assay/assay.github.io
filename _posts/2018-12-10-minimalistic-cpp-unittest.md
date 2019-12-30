---
layout: post
title: "Minimalistic C++ unittest framework"
feature-img: assets/img/pexels/programming.jpg
tags: [C++]
author-id: nettle
---


There are several very convenient and effective unittest libraries for C++.
However all of them tend to be large, sometimes heavy, stuffed with lots of
different features for all possible cases.

Sometimes, at least for me it happens from time to time, we need a very basic unittest functionality.
Especially if we have just started to develop a very simple tool or a library.
The idea to add [Googletest](https://github.com/google/googletest),
[Catch2](https://github.com/catchorg/Catch2),
[Cpputest](http://cpputest.github.io/),
[UnitTest++](https://github.com/unittest-cpp/unittest-cpp),
[CppUnit](https://www.freedesktop.org/wiki/Software/cppunit/),
[doctest](https://github.com/onqtam/doctest),
[Criterion](https://github.com/Snaipe/Criterion/)
or any of these feature-reach, powerful, easy-to-use, one-header frameworks sounds nice... but.
It will look like something really big (thousands of lines of code) are going to test something much much smaller.
A feeling like I need only 5% of functionality of these super nice frameworks.\\
That's why I usually use my minimalistic C++ unittest framework, I call it [miniunit](https://github.com/nettle/miniunit).

## Features

1. One header
2. ~150 lines of code (including comments)
3. No dependencies (includes only C++ headers \<string\>, \<vector\>, \<iostream\> and \<iomanip\>)
4. Extensible **TestCase** class
5. Extensible **TestSuite** class, customizable test launcher
6. **TEST** macro
7. **SKIP** marco

## Simple test example

Lest write a simple example:

* TEST1 to pass (returns `true`)
* TEST2 to fail (returns `false`)
* TEST3 to skip (use `SKIP` macro)
* TEST4 to throw exception

```cpp
#include "miniunit.h"  // TEST, SKIP, TestSuite, TestCase
#include <cstdio>      // printf

using namespace miniunit;

// Test PASS example
TEST(TEST1, "Test description") {
  return true;
}

// Test FAIL example
TEST(TEST2, "This test should fail") {
  return false;
}

// Test for SKIP example
TEST(TEST3, "Skip this test") {
  return false;
}

// Exception example
TEST(TEST4, "Throw exception") {
  throw "Oh my god!";
  return true;
}

// Test run example
int main(void) {
  SKIP(TEST3, "testing skip");

  bool result = TestSuite::run();

  printf("Result: %s\n", (result ? "PASS" : "FAIL"));
  return (result ? 0 : 1);
}
```

Save it as `test.cpp`.

## Default output

Now compile and run:
```shell
g++ --std=c++11 test.cpp -o test
./test
```

The output should be the following:
```
 [TEST1]      Test description : PASS
 [TEST2] This test should fail : FAIL
 [TEST3]        Skip this test : SKIP testing skip
 [TEST4]       Throw exception : FAIL Exception!
Result: FAIL
```

## Customization

The framework is very small and simple but we can customize it!
For instance we can add our own Test Case.
See how it can be done:

```cpp
// Custom test case
class MyTestCase : public TestSuite::TestCase {
public:
  MyTestCase(const char* n, const char* d)
    : TestSuite::TestCase(n, d) {
    // Add initialization code here
  }
  ~MyTestCase() {
    // Deinitialization code here
  }
  bool test() {
    // Test code
    return true;
  };
};

// Put test somewhere before test launcher
MyTestCase MyTestCase_instance("TEST5", "Custom test case");
```

However the most interesting part is test launcher customization.
We may not be satisfied with, for example, the format of the output.
Let's say we would prefer to see the output in a form of table.
No problem - we just rewrite `run()` method:

```cpp
// Custom test run function
class MyTestSuite : public TestSuite {
public:
  static bool run() {
    bool allResults = true;
    printf("| %-8s | %-30s | %-6s | %-20s |\n",
           "Test", "Description", "Result", "Comment");
    printf("| %-8s | %-30s | %-6s | %-20s |\n",
           std::string(8, '=').c_str(),
           std::string(30, '=').c_str(),
           std::string(6, '=').c_str(),
           std::string(20, '=').c_str());
    for (auto t : getTests()) {
      printf("| %-8s | %-30s |", t->name.c_str(), t->description.c_str());
      const char* resultStr = "OK";
      const char* reasonStr = "";
      if (!t->skip) {
        bool result = false;
        try {
          result = t->test();
        } catch (...) {
          reasonStr = "Exception!";
        }
        if (!result) resultStr = "Fail!";
        allResults = allResults && result;
      } else {
        resultStr = "Skip";
        reasonStr = t->reason.c_str();
      }
      printf(" %-6s | %-20s |\n", resultStr, reasonStr);
    }
    return allResults;
  };
};
```

But do not forget to call it instead of standard `TestSuite::run()` in `main()`:
```cpp
  bool result = MyTestSuite::run();
```

Now recompile and run `test` again. The output should be:
```
| Test     | Description                    | Result | Comment              |
| ======== | ============================== | ====== | ==================== |
| TEST1    | Test description               | OK     |                      |
| TEST2    | This test should fail          | Fail!  |                      |
| TEST3    | Skip this test                 | Skip   | testing skip         |
| TEST4    | Throw exception                | Fail!  | Exception!           |
| TEST5    | Custom test case               | OK     |                      |
Result: FAIL
```

## Source Code

Of course you can modify the code to add more functions, e.g. add exception handling
with stack backtrace, add argument parsing and smart logging etc.\\
The source code is available on [GitHub](https://github.com/nettle/miniunit)
as [miniunit.h](https://github.com/nettle/miniunit/blob/master/miniunit.h).
It also has this simple [demo.cpp](https://github.com/nettle/miniunit/blob/master/demo.cpp) code.
