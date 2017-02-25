# Bacovia

A symbolic math library for Sidef.

# EXAMPLE

```ruby
include('lib/bacovia.sf')

var x = Symbol('x')
var y = Symbol('y')

say x+y               #=> Sum(Symbol('x'), Symbol('x'))
say x-y               #=> Sum(Symbol('x'), Product(-1, Symbol('y')))
say x*y               #=> Product(Symbol('x'), Symbol('y'))
say x/y               #=> Product(Symbol('x'), Fraction(1, Symbol('y')))

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
```

# DESCRIPTION

As shown in the above example, it supports a variety of types, which described bellow:

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

# REQUIREMENTS

The library requires the Sidef programming language: [https://github.com/trizen/sidef](https://github.com/trizen/sidef)
