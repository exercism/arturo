# Tests

This track uses the [Unitt unit-testing package][unitt], installed automatically when running the tests.
From within the exercise folder, run `exercism test` or `arturo tester.art` to run your solution against the test suite.

If you haven't written any code, the test suite will fail with a message like:

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

Replace the `panic "please implement the <some-function-name> function"` line in `src\<your-exercise>.art` with your solution.
Then rerun the test suite, and you should see something like:

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

The output lists the test file path, the name of the test suite, and the test case assertions, reporting whether a test had passed (✅), failed (❌) or was skipped (⏩). 

The following test file has three tests, one of which is skipped.
Unskip a test by replacing `test.skip` with `test` beside the description for the test.

```arturo
import.version:1.1.2 {unitt}!
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

If we rerun the tests again, the second test is run and passes, but the third test is still skipped.


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

A failed test would look like this

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
```

Once all tests pass, you can submit your solution using `exercism submit`.

[packager]: https://pkgr.art/
