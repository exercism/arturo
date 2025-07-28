# Instructions append

## `Print` does not quote string values

This exercise involves manipulating numeric scores.
#[a: 1]` and `#[a: "1"]` are not the same:

```arturo
inspect #[a: 1]
; [ :dictionary
;        a  :        1 :integer
; ]

inspect #[a: "1"]
; [ :dictionary
;        a  :        1 :string
; ]
equal? #[a: "1"] #[a: 1]
; false
```

A common debugging practice is to `print` values.
However, the output will not add quote marks around strings.
Therefore, a numeric string like `"1"` when printed appears the same as the integer `1`.

```arturo
print #[a: 1]
; [a:1]
print #[a: "1"]
; [a:1]
```
In the test output for this exercise, you may see a result like `:x: equal? [a:1 e:1 i:1 o:1 u:1] [a:1 e:1 i:1 o:1 u:1]`.
The two dictionaries being compared appear the same when printed.
However, the first dictionary has numeric string values and the second one has integer values so they are not the same. 
When debugging, `inspect` can be used to check the contents of your dictionary.

## `Express` does quote string values

`express` converts a value to Arturo code and returns a string representing that code representation.
In that result, any string values will be quoted.
As a result, `express "1"` will return `"1"`, not `1`.

```arturo
express #[name: "Octavius" age: 22]
; #[name: "Octavius" age: 22 ]
```
```arturo
express #[name: "Octavius" age: "22"]
; #[name: "Octavius" age: "22" ]
```
