# Bacovia

A symbolic math library for Sidef.

# EXAMPLE

```ruby
include('lib/bacovia.sf')

var x = Symbol('x')
var y = Symbol('y')

say x+y               #=> Sum(Symbol('x'), Symbol('y'))
say x-y               #=> Sum(Symbol('x'), Product(-1, Symbol('y')))
say x*y               #=> Product(Symbol('x'), Symbol('y'))
say x/y               #=> Fraction(Symbol('x'), Symbol('y'))

say x**y              #=> Power(Symbol('x'), Symbol('y'))

say Log(x)            #=> Log(Symbol('x'))
say Log(x)+Log(y)     #=> Log(Product(Symbol('x'), Symbol('y')))

say Exp(x)            #=> Exp(Symbol('x'))
say Exp(x)*Exp(y)     #=> Exp(Sum(Symbol('x'), Symbol('y')))


say "\n=> Summation fraction:"
var sum = Fraction(0, 1)

for n in (1..10) {
    sum += Fraction(1, n)
}
say sum                     #=> Fraction(10628640, 3628800)
say sum.numeric.as_frac     #=> 7381/2520


say "\n=> Product fraction:"
var prod = Fraction(1, 1)

for n in (0..3) {
    prod *= Exp(Fraction(1, n!))
}
say prod                    #=> Product(Fraction(1, 1), Exp(Fraction(1, 1)), Exp(Fraction(1, 1)), Exp(Fraction(1, 2)), Exp(Fraction(1, 6)))
say prod.numeric            #=> 14.39191609514989


say "\n=> Alternative representations:"
Power(3, 5).alternatives.each { .say }    #=> [Exp(Product(Log(3), 5)), Power(3, 5), 243]
```

# DESCRIPTION

As shown in the above example, it supports a variety of types, which are described bellow:

* Symbol
    - symbolic value: `Symbol(name)`
* Fraction
    - symbolic fraction: `Fraction(numerator, denominator)`
* Power
    - symbolic exponentiation: `Power(base, power)`
* Log
    - symbolic natural logarithm: `Log(x)`
* Exp
    - symbolic natural exponentiation: `Exp(x)`
* Sum
    - symbolic sum: `Sum(a, b, c)`
* Product
    - symbolic product: `Product(a, b, c)`

Each type communicates with all the other types recursively.

The library also has built-in support for alternative representations (provided by the method `.alternatives`),
which uses common mathematical identities to symbolically create equivalent expressions from the self-expression.

# SPECIAL METHODS

The special methods provided by this library:

* `.alternatives()`
    - returns an array with alternative representations of the self-expression.
* `.simplify()`
    - returns a simplification of the self-expression.
* `.pretty()`
    - returns a human-readable stringification of the self-expression.


Example for `.alternatives()`:

```ruby
Exp(Log(3) * 2).alternatives.each { .say }
```

Output:

```ruby
Exp(Product(Log(3), 2))
Power(3, 2)
9
```

Example for `.simplify()`:

```ruby
say Log(Log(Log(Exp(Exp(Exp(Symbol('x'))))))).simplify
```

Output:

```ruby
Symbol('x')
```

Example for `.pretty()`:

```ruby
say Power(3, Log(Fraction(1, 2))).pretty
```

Output:
```ruby
say 3^log(1/2)
```

# REQUIREMENTS

The library requires the Sidef programming language: [https://github.com/trizen/sidef](https://github.com/trizen/sidef)
