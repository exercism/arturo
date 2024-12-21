# Track-specific information

In this exercise, you will be expected to return the ages using a [physical quantity] with a custom unit representing the length of a single year on a that planet.
In Arturo, a quantity consists of a numerical amount and an associated [unit of measurement][unit-of-measurement].

```arturo
length: 10`m
units length ; `m
scalar length ; 10

10`m * 10`m ; 100 m²
```

~~~~exercism/caution
Arturo's built-in `yr unit converts to 31556952 seconds.
Therefore, you'll need to define and use your own year unit in terms of the number of seconds referenced previously in the instructions.
~~~~

Quantities can be [converted][convert] to another compatible unit.
```arturo
convert 1`m `ft ; 1250/381 ft
convert 100`m2 `ft2 ; 156250000/145161 ft²

property `m  ; length
property `m2 ; area

convert 1`m `m2 ; conversion error results
```

~~~~exercism/note
Because of the precision limitations with floating point numbers, Arturo sometimes stores the scalar as a rational number.
The `to` function can be used to retrieve the amount instead as an approximate floating point number.

```arturo
length: convert 1`m `ft ; 1250/381 ft
to :floating length ; 3.280839895013123
```
~~~~

Arturo also allows us to [specify] our own units for quantities.

```arturo
specify 'nauMile 1.151`mi
property `nauMile length
specify 'lea 3.00579`nauMile
property `lea ; length
depth: 20000`lea
convert depth `km ; 111355.7993425152 km
```

[physical-quantities]: https://en.wikipedia.org/wiki/Physical_quantity  
[unit-of-measurement]: https://en.wikipedia.org/wiki/Unit_of_measurement
[convert]: https://arturo-lang.io/master/documentation/library/quantities/convert/
[specify]: https://arturo-lang.io/master/documentation/library/quantities/specify/
