# Bacovia

A new symbolic math library for Sidef.

# DESCRIPTION

It supports a variety of types, such as:

* Symbol
    - e.g.: `Symbol(name)`
* Fraction
    - e.g.: `Fraction(numerator, denominator)`
* Power
    - e.g.: `Power(base, power)`
* Log
    - e.g.: `Log(x)`
* Exp
    - e.g.: `Exp(x)`
* Sum
    - e.g.: `Sum(a, b, c)`
* Product
    - e.g.: `Product(a, b, c)`

Each type communicates with all the other types recursively.

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

# REQUIREMENTS

The library requires the Sidef programming language: [https://github.com/trizen/sidef](https://github.com/trizen/sidef)
