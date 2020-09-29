+++
title = "Who Needs Floating-Point Anyway?"
date = 2020-09-29
description = "Suppose we truly want floating point arithmetic free of rounding error..."
[extra]
category = "Floating-Point"
+++

Suppose we truly want floating point arithmetic free of rounding error. Can we
do this for all combinations of floating point numbers? Well. Let's for now
just consider finite arithmetic; that is, neither infinity nor NaN. In this
case, all we need to do is define the smallest positive floating point number
as "1", and shift the decimal point accordingly. According to the IEEE-754
standard, for double-precision this number is

2<sup>-1074</sup>

which in binary looks like
```
0 00000000000 0000000000000000000000000000000000000000000000000001
```

To treat this as "1" we must also look at what the largest number is.
Checking IEEE-754, we have

2<sup>1023</sup> × (1 + (1 − 2<sup>−52</sup>)), or in bits,

```
0 11111111110 1111111111111111111111111111111111111111111111111111
```

Putting this together, we need to represent a number as large as

2<sup>1023</sup> × (1 + (1 − 2<sup>−52</sup>)) / (2<sup>−1074</sup>).

Which, we can calculate with the useful `bc` (with sufficiently high `scale`)
as
```
36385714125121573300846800698456749842842774431060269030973563199251\
83520276313187422051044619975257814616895952553597550412366074125973\
05594915359190782200698392412987448013052928786408355279308639946743\
57611588999020693594474762898847930291552594690170203187215045688094\
95566077392257613796983034261186022501993558219960112146924922314987\
24661213715671558623030843303146025660694164325513330061947744775142\
60351201969859368060220131234488198148976536169638305696900504838830\
71976087551424621650897680388272858267735217700412928884785446308400\
63729813907563445195499310977439636039716323348918368319786868700433\
55177324550146752512
```
So, to fit everything inside a fixed-point value, we need the base-2 logarithm
of this:

```
$ bc -l
scale=60;
l(2^1023 * (1 + (1 - 2^-52)) * 2^1074)/l(2)
$ 2097.999999999999999839828674809254106809409981385123854002550379
```
Which is just a tad under 2098 bits. But remember, we need negative numbers as
well so we need **2099** bits to get the sign for twos-complement. Then, once we
have some value in fixed-point one can multiply it by 2<sup>-1074</sup> to get
the correct value. What purpose does this have? For example, the [GNU
MPFR](https://www.mpfr.org/) library has arbitrary-precision floating point values.
Knowing that we need 2099 bits means we can use any value with at least 2099 bits
of precision to do any sequence of floating point operations with _no error_,
as long as the results are correctly rounded. MPFR is carefully designed to be
[correctly rounded](https://hal.inria.fr/inria-00070266/document), so that's
covered for us too!

