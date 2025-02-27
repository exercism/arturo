# Tests

This track uses the [Unitt unit-testing package][unitt].
If not already installed, Arturo will download this package automatically at runtime.

To run tests, navigate to the exercise folder in your terminal and run either `arturo tester.art` or `exercism test`.

Each exercise folder contains three key files:
    `src/<exercise-name>.art` contains the solution to be tested.
    `tests/test-<exercise-name>.art` contains the exercise tests 
    `tester.art` is the testing entry-point which runs and reports the tests inside `tests/test-<exercise-name>.art`.


## Test Structure


`tests/test-<exercise-name>.art` contains the test cases for the exercise.
These tests are organized into one or more test suites.
Each test suite is defined with the `suite` word and contains one or more test cases defined with the `test` word.
After the first test case, all test cases are initially skipped with the `skip` attribute.
Replace `test.skip` with `test`, removing the `skip` attribute, for the test case you want to unskip.

Withn each test case, there will be a descriptive message which is reported when the test case is run.
There will also be one or more assertions comparing an expected value (on the left) to a value returned by your code (on the right).

For example, the following code is a reduced test suite for the Leap exercise.

```arturo
import {unitt}!
import {src/leap}!

suite "Leap" [
    test "a year not divisible by 4 is a common year" [
        result: isLeap? 2015
        assert -> false = result
    ]

    test.skip "a year divisible by 2 and not divisible by 4 is a common year" [
        result: isLeap? 1970
        assert -> false = result
    ]

    test.skip "a year divisible by 4 and not divisible by 100 is a leap year" [
        result: isLeap? 1996
        assert -> true = result
    ]
]
```

After both `unitt` and your Leap solution is imported, Arturo evaluates the "Leap" suite, encountering three tests.
Each test has a description and a message, but only the first one will be run.

## Test Output

Looking at the Leap exercise, let's see what the output of running the test suite is.
Let's use the following solution as a starting point.

```arturo
isLeap?: function [year][
    panic "please implement the isLeap? function"
]
```

If we run the tests now, Arturo will panic while evaluating the first test.
Since it was unsuccessful in evaluating the first test, it will not continue to evaluate the other tests.
It will also report 0 assertions encountered due to this issue, looking something like this:

```plaintext
===== tests\test-leap.art =====

Suite: Leap 


══╡ Program Error ╞═════════════════════════════════════════════════ <script> ══

  please implement the isLeap? function



===== Statistics =====

⏏️    TOTAL: 0 assertions
✅  PASSED: 0 assertions
⏩ SKIPPED: 0 assertions
❌  FAILED: 0 assertions

===== ========== =====
```


At this point, we need to remove the panic and replace it with some code that will pass the first test.


```arturo
isLeap?: function [year][
    false
]
```

If we rerun the tests, we will see output (below) that the first test passes, but the other two tests are skipped.
The test description and assertions are reported with a leading emoji denoting a passed test (✅), a failed test (❌), or a skipped test (⏩).
Under the statistics section, the total number of passing or failed assertions is reported, followed by the number of passed assertions, the number of skipped assertions, and finally the number of failed assertions.

```plaintext
===== tests\test-leap.art =====

Suite: Leap

    ✅ - assert that a year not divisible by 4 is a common year
         assertion: false = false

    ⏩ - assert that a year divisible by 2 and not divisible by 4 is a common year 
         skipped!

    ⏩ - assert that a year divisible by 4 and not divisible by 100 is a leap year
         skipped!

===== Statistics =====

⏏️    TOTAL: 1 assertions
✅  PASSED: 1 assertions
⏩ SKIPPED: 2 assertions
❌  FAILED: 0 assertions

===== ========== =====
```


Unskipping the second test, we'll have the following tests:

```arturo
import {unitt}!
import {src/leap}!

suite "Leap" [
    test "a year not divisible by 4 is a common year" [
        result: isLeap? 2015
        assert -> false = result
    ]

    test "a year divisible by 2 and not divisible by 4 is a common year" [
        result: isLeap? 1970
        assert -> false = result
    ]

    test.skip "a year divisible by 4 and not divisible by 100 is a leap year" [
        result: isLeap? 1996
        assert -> true = result
    ]
]
```


If we rerun the tests again, the second test passes, but the third test is still skipped.


```plaintext
===== tests\test-leap.art =====

Suite: Leap

    ✅ - assert that a year not divisible by 4 is a common year
         assertion: false = false

    ✅ - assert that a year divisible by 2 and not divisible by 4 is a common year 
         assertion: false = false

    ⏩ - assert that a year divisible by 4 and not divisible by 100 is a leap year
         skipped!

===== Statistics =====

⏏️    TOTAL: 2 assertions
✅  PASSED: 2 assertions
⏩ SKIPPED: 1 assertions
❌  FAILED: 0 assertions

===== ========== =====
```


Let's unskip the third test and run the tests again.
At this point, we'll encounter a failing test because the third test expects `true`, not `false`.


```plaintext
===== tests/test-leap.art =====

Suite: Leap 
 
    ✅ - assert that a year not divisible by 4 is a common year 
         assertion: false = false

    ✅ - assert that a year divisible by 2 and not divisible by 4 is a common year 
         assertion: false = false

    ❌ - assert that a year divisible by 4 and not divisible by 100 is a leap year 
         assertion: true = false




===== Statistics =====

⏏️    TOTAL: 3 assertions
✅  PASSED: 2 assertions
⏩ SKIPPED: 0 assertions
❌  FAILED: 1 assertions

===== ========== =====


══╡ Program Error ╞══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════ <script> ══

  Some tests failed!
```

At this point, we need to fix the code to pass the third test. Once that's done, we can rerun the tests and see that all tests pass.

```plaintext
===== tests/test-leap.art =====

Suite: Leap 
 
    ✅ - assert that a year not divisible by 4 is a common year 
         assertion: false = false

    ✅ - assert that a year divisible by 2 and not divisible by 4 is a common year 
         assertion: false = false

    ✅ - assert that a year divisible by 4 and not divisible by 100 is a leap year 
         assertion: false = false




===== Statistics =====

⏏️    TOTAL: 3 assertions
✅  PASSED: 3 assertions
⏩ SKIPPED: 0 assertions
❌  FAILED: 0 assertions

===== ========== =====
```

At this point, your solution can be submitted using `exercism submit` and the online test runner will test your code.
The online test runner unskips and runs all the tests every time so make sure you're not skipping any tests before submitting.

[unitt]: [https://unitt.pkgr.art/]
