
## How to Calculate Single Variable Definite Integrals

### Install SciPy

Before we start, we need to install the SciPy module. It provides a collection of Mathematical algorithms and functions that we'll use.

To calculate single variable definite integrals, we need to first import `quad` from `scipy.integrate`. It is a general purpose function used to calculate single variable definite integrals.

```python
from scipy.integrate import quad
```

### Elementary Functions

From there, we'll need to define the integrand as a function in Python.

For example, if we wanted to calculate the integral of x-squared, we would define the integrand as a Python function like so:

```python
def integrand(x):
    return x**2
```

Once we define the integrand, we can calculate the definite integral using the quad function like this:

```python
print(quad(integrand, 0, 1))
# (0.33333333333333337, 3.700743415417189e-15)
```

![[Pasted image 20251204200002.png]]


In this example, we calculate that the estimated result of the integral from 0 to 1 of x-squared is approximately 0.333 with an absolute error of roughly 3.7e-15.

The quad function returns a tuple of an estimation of the definite integral followed by the absolute error of the estimation.

What the `quad` function does is essentially evaluate the `integrand` function at multiple different values between our limits of integration to be able to calculate an estimate of the integral.

Another example would be if I wanted to calculate the integral of `(x+1)/x**2`. We would first define it as a function in Python, and pass it into the `quad` function along with the limits of integration:

```python
from scipy.integrate import quad

def integrand(x):
    return(x+1)/x**2

print(quad(integrand, 1, 2))
# (1.1931471805599452, 1.3246594716242401e-14)
```

### Other Common Functions

If we wanted to use common mathematical functions such as `sin(x)` or `log(x)`, we can use another Python package for scientific computing – NumPy. You can install the package using the following command:

## How to Calculate Multi-Variable Integrals

### Double Integrals

To calculate double integrals, we need to import the `dblquad` function from `scipy.integrate`:

```
from scipy.integrate import dblquad
```

We define the integrand in a similar way to definite it with one variable, only this time we specified two arguments instead.

```python
def integrand(y, x):
    return x*y**2
```

We can then calculate the definite integral using the `dblquad` function given by `scipy`.

Note that the integrand is a function that needs to accept `y` as the first parameter and `x` as the second parameter.

```python
print(dblquad(integrand, 0, 1, 2, 4))
# (9.333333333333334, 2.0679162295394134e-13)
```

### Variable Limits

To calculate integrals with variable limits, we'll need to define functions for the lower and upper limits of integration for y in terms of x:

```python
def upper_limit_y(x):
    return x**2

def lower_limit_y(x):
    return x

def integrand(y, x):
    return x+y

print(dblquad(integrand, 0, 2, lower_limit_y, upper_limit_y))
```

In this example, we calculate that the estimated result of the double integral of x+y from x = 0 to x = 2, and from y = x to y = x^2 is approximately 3.2 with an absolute error of roughly 1.10e-13.

### Triple Integrals

To calculate triple integrals, we can use the `tplquad` function:

```python
from scipy.integrate import tplquad

def integrand(z, y, x):
    return z*(x+y+z)

print(tplquad(integrand, 0, 1, 4, 5, 0, 1))
# (2.8333333333333335, 3.6983326566167174e-14)
```

The function requires us to pass in similar arguments, being the upper and lower limits of integration in `x`, `y` and `z`.

In this example, we calculate that the estimated result of the triple integral of z multiplied by (x+y+z) from x = 0 to x = 1, y = 4 to y = 5, and z = 0 to z = 1 is approximately 2.83 with an absolute error of 3.70e-14:

## How to Evaluate Single Variable Indefinite Integrals

To calculate single variable indefinite integrals with Python, we need to use the SymPy library. It's used for symbolic computation and involves exact computation using variables. To install it, install the SymPy module:

```
pip install sympy
```

Once it has been installed, we can import the `Symbol` and `integrate` methods from `sympy`:

```python
from sympy import Symbol, integrate
```

We first need to define the variables used in the integrand:

```python
x = Symbol('x')
```

After that, we can integrate the function using the `integrate` method that SymPy provides. It expects two arguments: the first is the integrand, and the second is the variable we are integrating with respect to.

For example, if we wanted to integrate x-squared with respect to `x`, we can define the integrand in Python as `x**2`:

```python
print(integrate(x**2, x))
# (x**3)/3
```

