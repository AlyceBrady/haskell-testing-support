# haskell-testing-support: Haskell Test Suite Support Module

The TestSuiteSupportModule defines a new type, a TestItem, that
can be used to organize and display single tests and test suites.
The display for each single test or each test case in a test suite
includes a description of the test and whether it passed or failed.

Use the TestSuite constructor to create a test suite object,
providing a description of the test suite and a list of test
items (single tests or nested test suites).  Use the Test
constructor to make a test item out of a boolean expression, again
providing a description.  The boolean expression should evaluate
to True when the test it represents passes.
For example, 
```
   example1 = TestSuite "An empty test suite" []
   example2 = TestSuite "A suite with a single test"
                        [ Test "test1" boolExpr ]
      where boolExpr is some boolean expression such as
          (callToFunctionToTest == expectedResult)
      Example:
          concreteEx2 = TestSuite "Concrete suite with single test"
                           [ Test "The test" (reverse [1, 2] == [2, 1]) ]
   example3 = TestSuite "A suite with multiple tests"
              [ Test "1" boolExpr1, Test "2" boolExpr2, Test "3" boolExpr3 ]
   example4 = TestSuite "A suite with tests and nested suites"
                [ Test "test1" boolExpr1, example1, example2 ]
```
In these examples, the identifiers example1, ..., example4 are
zero-parameter functions that each evaluate to a specific test suite.

To run a test suite and display its results, simply type the
identifier associated with the test suite.  For example,
typing
```
     concreteEx2
```
would show the following results:
```
     Concrete suite with single test
       The test: Passed
```

This module also defines the runTest function which evaluates
to a single boolean value representing whether the test passed
or not.  If the test item passed to runTest is an entire test
suite, the function returns True if all the tests passed, in
other words, if all the tests in the suite evaluated to True,
and returns False if any test in the suite failed.
For example,
```
   runTest example3
```
would return true if all three tests in the suite passed.

Author: Alyce Brady

November 2003
