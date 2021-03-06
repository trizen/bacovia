# Bacovia

A symbolic math library for Sidef.

# EXAMPLE

```ruby
include('lib/bacovia.sf')

var x = Symbol('x')
var y = Symbol('y')

say x+y               #=> Sum(Symbol('x'), Symbol('y'))
say x-y               #=> Difference(Symbol('x'), Symbol('y'))
say x*y               #=> Product(Symbol('x'), Symbol('y'))
say x/y               #=> Fraction(Symbol('x'), Symbol('y'))

say x**y              #=> Power(Symbol('x'), Symbol('y'))

say Log(x)            #=> Log(Symbol('x'))
say Log(x)+Log(y)     #=> Log(Product(Symbol('x'), Symbol('y')))

say Exp(x)            #=> Exp(Symbol('x'))
say Exp(x)*Exp(y)     #=> Exp(Sum(Symbol('x'), Symbol('y')))


say "\n=> Sum:"
var sum = Fraction(0, 1)

for n in (1..10) {
    sum += Fraction(1, n)
}
say sum                     #=> Fraction(10628640, 3628800)
say sum.numeric.as_frac     #=> 7381/2520


say "\n=> Product:"
var prod = Fraction(1, 1)

for n in (0..3) {
    prod *= Exp(Fraction(1, n!))
}
say prod                    #=> Product(Fraction(1, 1), Exp(Fraction(1, 1)), Exp(Fraction(1, 1)), Exp(Fraction(1, 2)), Exp(Fraction(1, 6)))
say prod.numeric            #=> 14.39191609514989...


say "\n=> Alternative representations:"
Power(3, 5).alternatives.each { .say }    #=> [Exp(Product(Log(3), 5)), Power(3, 5), 243]
```

# DESCRIPTION

The types supported by this library are described bellow:

#### # `Symbol(name, value=nil)`

Represents a symbolic value. Optionally, it can have a numeric value.

#### # `Fraction(numerator, denominator)`

Represents a symbolic fraction.

#### # `Difference(minuend, subtrahend)`

Represents a symbolic difference.

#### # `Power(base, power)`

Represents a symbolic exponentiation in a symbolic base.

#### # `Log(x)`

Represents the natural logarithm of a symbolic value.

#### # `Exp(x)`

Represents the natural exponentiation of a symbolic value.

#### # `Sum(a, b, c, ...)`

Represents a summation of an arbitrary (finite) number of symbolic values.

#### # `Product(a, b, c, ...)`

Represents a product of an arbitrary (finite) number of symbolic values.

# SPECIAL METHODS

An interesting feature is the support for alternative representations (provided by the method `.alternatives`),
which uses common mathematical identities to create symbolically equivalent expressions from the self-expression.

Bellow we describe the special methods provided by this library:

#### # `.alternatives()`

Returns an array with alternative representations from the self-expression.

```ruby
Exp(Log(3) * 2) -> alternatives.each { .say }
```

Output:

```ruby
Exp(Product(Log(3), 2))
Power(3, 2)
9
```

#### # `.simple()`

Returns a simplification of the self-expression.

```ruby
Exp(Log(Log(Exp(Exp(Log(Symbol('x'))))))) -> simple.say
```

Output:

```ruby
Symbol('x')
```

#### # `.pretty()`

Returns a human-readable stringification of the self-expression.

```ruby
Power(3, Log(Fraction(1, 2))) -> pretty.say
```

Output:
```ruby
3^log(1/2)
```

#### # `.numeric()`

Evaluates the self-expression numerically and returns the result as a Number or a Complex object.

```ruby
var x = Symbol('x')
var expr = (x**2 - x + 41)

for n in (1..3) {
    x.value = n              # sets `x` to the value of `n`
    say expr.numeric         # evaluates the expression numerically
}
```

Output:
```ruby
41
43
47
```

# REQUIREMENTS

The library requires the Sidef programming language: [https://github.com/trizen/sidef](https://github.com/trizen/sidef)
