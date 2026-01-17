# Instructions append

## Some notes about Arturo strings

You'll see some syntax in the tests that may be new to you: multiline strings enclosed in `{ braces }`.

### References

* [`:string` type][string] in the Language reference.
* [Basic Usage][usage] documentation in the Strings module.

[string]: https://arturo-lang.io/documentation/language/#string
[usage]: https://arturo-lang.io/documentation/library/strings/#basic-usage

### Arturo string literals

Arturo has a few ways to write string literals:

1. Single-line strings enclosed in double quotes

    ```arturo
    greeting: "Hello, World!"

    print express greeting     ; => "Hello, World!"
    ```

1. Line-ending strings using a "smart quote" `«`

    ```arturo
    farewell: « Goodbye, Mars!

    print express farewell     ; => "Goodbye, Mars!"
    ```

   These can be nicely readable if you have a list of short strings:

    ```arturo
    numberWords: [
        « one
        « two
        « three
        « four, and so on
    ]
 
    print express numberWords    ; => ["one" "two" "three" "four, and so on"]
    ```

1. Multi-line strings enclosed in braces.
   The "common" indentation will be removed.
   Leading and trailing newlines are removed.

    ```arturo
    multiline: {
        First line
        Second line
            Third line keeps indentation
        Last line!


    }

    print express first multiline   ; => 'F'
    print express last multiline    ; => '!'
    lines: split.lines multiline
    print size lines                ; => 4
    print express lines\2           ; => "    Third line keeps indentation"
    ```

1. Verbatim strings are preserved exactly, including leading/trailing whitespace

    ```arturo
    code: {:
        greet: function [name][
            print ~"Hello, |name|~"

        greet "World""
    :}

    print ">" ++ code ++ "<"
    print express first code
        ; => prints a literal newline character between single quotes
    print express (split.lines code | get 1)
        ; => "    greet: function [name]["
    ```

1. Heredoc-style strings reside below a line of 3 or more hyphens until the end of the file.
   This acts the same as Perl's `__DATA__` keyword.
   This style would be useful in a module, where you might store documentation or the license text in a variable at the end of the file.

    If this is in a file named "mymodule.art"

    ```arturo
    myLicense:
    ---------
    This text has been placed in the public domain.
    Do with it what you will.
    ```

    Then

    ```arturo
    import {mymodule}!
    print ~">|myLicense|<"  ; => >This text has been placed in the public domain.
                            ; => Do with it what you will.<
    ```
