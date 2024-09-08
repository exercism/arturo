# Tests

This track uses the [unitt unit-testing framework][unitt].

Each exercise will have a similar structure as seen below:

```
HELP.md
README.md
src
tester.art
tests
```

To run the exercise's test suite on the CLI, run `arturo tester.art` (or `exercism test`) inside the exercise folder.

## Structure

Your solution goes inside `src\<slug>.art` where `slug` is the exercise slug.
For the Leap exercise, this is `leap` so your solution goes into `src\leap.art`.

`tester.art` is what Unitt calls a runner which is responsible for locating, finding, and running the tests for each exercise.
The runner looks inside the `tests` folder to find the test file at `tests\test-<slug>.art` or `tests\test-leap.art` as an example.

This test file contains one or more test suites, noted by the `suite` word and grouping similar tests, each noted by the `test` word.
The first test is run every time, but subsequent tests are marked with a `skip` attribute.
To run a skipped test, change `test.skip` to `test` for that test and rerun the test suite as documented above.
Once all tests pass locally, you can submit your solution with `exercism submit` inside the exercise folder.

## Test Output

Let's use the following example test file to look at the Unitt test output from running `tester.art`.

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

If we use the starting code in `src\leap.art` without modification,
running `exercism test` will print out the text below.
The starting code contains panics that need to be replaced with our own code.
These panics identify what code needs to be implemented

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

Each test may have one or more assertions, but 0 assertions are reported because Arturo panics before the entire test suite can be processed.

At this point, we should write some code to pass the first test. When we rerun the tests, we might seen something like this:

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

The output prints out the test suite named "Leap" and the results of our two tests.
For each test, we see a visual symbol for whether that test passed, failed, or was skipped, then the test description, and the values tested on the next line. 
The expected value is on the left side of the `=` and the returned value is on the right side.

The statistics section will report the total assertions encountered, the total passed, the total skipped, and the total failed.

Once all assertions pass, your solution can be submitted using `exercism submit`.
The online test runner unskips all tests when checking your solution so a locally passing solution might not pass online.

[unitt]: [https://unitt.pkgr.art/]
