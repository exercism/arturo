# Instructions append

## Arturo instructions

For this exercise, you'll need to support two different ways of calling the `stringify` word:

1. With the `roman` attribute (e.g. `stringify.roman 3999`)
2. Without the `roman` attribute (e.g. `stringify 3999`)

For more information, check the [attributes][attributes] documentation as well as the [`attr`][attr] documentation.

~~~~exercism/caution
In addition to `attr`, the `attrs` function is useful: it returns all the attributes of the function call as a dictionary.

Beware that these two functions are destructive!

The implementation of Arturo uses an ["attributes table"][createAttrsStack].

* `attrs` [explicitly empties the table][getAttrsDict] after retrieving the attributes.
* `attr` [removes ("pops") the attribute from the table][builtinAttr].

An example:

```arturo
showAttributes: function [x][
    print attr 'question
    print attrs
    print attrs
]

showAttributes .question:"6 * 9" .answer:42 'arg
```
outputs
```
6 * 9
[answer:42]
[]
```

At each step, we see the attribute dictionary shrink.

**Conclusion**: be aware that you can only fetch attributes once.
If you need to refer back to attributes, capture them at the start of your functions.

[getAttrsDict]: https://github.com/arturo-lang/arturo/blob/2ef0081570feb6ab752404c32bbf85132df379fb/src/vm/stack.nim#L187
[builtinAttr]: https://github.com/arturo-lang/arturo/blob/2ef0081570feb6ab752404c32bbf85132df379fb/src/library/Reflection.nim#L85
[createAttrsStack]: https://github.com/arturo-lang/arturo/blob/2ef0081570feb6ab752404c32bbf85132df379fb/src/vm/stack.nim#L136
~~~~

[attributes]: https://arturo-lang.io/latest/documentation/language/#attributes
[attr]: https://arturo-lang.io/latest/documentation/library/reflection/attr/
