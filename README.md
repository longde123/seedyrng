SeedyRNG
========

SeedyRNG (Seedy) is a pseudorandom number generator library for Haxe.

Seedy is intended for generating numbers for applications that require reproducible sequences. Such examples include video game world generation or unit tests.

It provides a general featured interface such as producing an integer within a range or choosing an item from an array. It also allows you to use your own generator implementation if you desire.

Seedy is deterministic or predictable which means it is *not* suitable for secure cryptographic purposes.

Quick start
-----------

Install it from Haxelib:

    haxelib install seedyrng

To install the latest using `haxelib git`.

If you simply need a random integer:

```haxe
Seedy.randomInt(0, 10); // => Int
```

If you need finer control, such as specifying the seed, use an instance of `Random`:

```haxe
var random = new Random();
random.setStringSeed("hello world!");
random.randomInt(0, 10); // => Int
```

By default, the generator is xorshift128+. It is a relatively new generator based on the xorshift family. It is comparable to the popular Mersenne Twister but it is faster and simpler.

If you want to use another generator, you can specify it on the constructor:

```haxe
var random = new Random(new GaloisLFSR32());
```

For details on all the methods, see the [API documentation](https://chfoo.github.io/seedyrng/api/).

Randomness testing
------------------

If you desire, you can statistically test the generator using something like:

    haxe hxml/app.cpp.hxml && out/cpp/Seedy | diehard -g 200 -a

Alternatively, you can [inspect a visualization](https://unix.stackexchange.com/a/289670) of the output:

    export X=1000 Y=1000; haxe hxml/app.cpp.hxml && out/cpp/Seedy | head -c "$((3*X*Y))" | display -depth 8 -size "${X}x${Y}" RGB:-
