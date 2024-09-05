# Tests

This track uses the [unitt unit-testing framework][unitt] which should be installed automatically when you run the tests.
Some tests are skipped by default when working offline, but all tests are run by the online test runner.

```
.../arturo/hello-world
HELP.md
README.md
src
tester.art
tests
```

Each exercise folder contains a `tester.art` entry point (see below).
To run the exercise's test suite on the CLI, run `arturo tester.art` (or `exercism test`).

This file imports the `unitt` package and runs the test file inside the tests folder.
This test file is named `test-<slug>.art` and contains one or more test suites.
Each test suite contains one or more tests which test your submitted code in `src\<slug>.art`.
The first test will run every time but subsequent tests are initially marked as `test.skip`.
Remove the `.skip` attribute and run the tests again.


## Test Output

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
]
```

This test file defines a single test suite named Leap with two tests, one that runs and one that is skipped.
Running `arturo tester.art` without changing code in `src\leap.art` results in the following output.

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

0 tests are encountered because the track has Arturo panic if isLeap? hasn't been implemented (i.e. add your code)

At this point, we should write some code that passes the first test and rerun our code.
In the output, the expected value is on the left side of the `=` and the returned value is on the right side.

```plaintext
===== tests\test-leap.art =====

Suite: Leap

    ✅ - assert that a year not divisible by 4 is a common year
         assertion: false = false

    ⏩ - assert that a year divisible by 2 and not divisible by 4 is a common year 
         skipped!




===== Statistics =====

⏏️    TOTAL: 1 assertions
✅  PASSED: 1 assertions
⏩ SKIPPED: 1 assertions
❌  FAILED: 0 assertions

===== ========== =====
```

We've passed the first test but `unitt` indicates there's a skipped test so we'll unskip it.

```
===== tests\test-leap.art =====

Suite: Leap 

    ✅ - assert that a year not divisible by 4 is a common year
         assertion: false = false

    ❌ - assert that a year divisible by 2 and not divisible by 4 is a common year
         assertion: false = true




===== Statistics =====

⏏️    TOTAL: 2 assertions
✅  PASSED: 1 assertions
⏩ SKIPPED: 0 assertions
❌  FAILED: 1 assertions

===== ========== =====


══╡ Program Error ╞══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════
  Some tests failed!
```

The second test failed because we haven't written the code to make it pass.
Once we update our code and rerun it, we should see a passing second test.

```plaintext
===== tests\test-leap.art =====

Suite: Leap 

    ✅ - assert that a year not divisible by 4 is a common year
         assertion: false = false

    ✅ - assert that a year divisible by 2 and not divisible by 4 is a common year
         assertion: false = false




===== Statistics =====

⏏️    TOTAL: 2 assertions
✅  PASSED: 2 assertions
⏩ SKIPPED: 0 assertions
❌  FAILED: 0 assertions

===== ========== =====
```

At this point, all tests are passing so we can submit our solution to the website.

[unitt]: [https://unitt.pkgr.art/]
