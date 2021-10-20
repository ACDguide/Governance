# Applying conventions to your files

## Coordinate system

```{dropdown} coordinate variable
A coordinate variable is a one-dimensional variable with the same name as a dimension, which names the coordinate values of the dimension. It must not have any missing data (for example, no _FillValue or missing_value attributes) and must be strictly monotonic (values increasing or decreasing). A two-dimensional variable of type char is a string-valued coordinate variable if it has the same name as its first dimension, e.g.: char time( time, time_len); all of its strings must be unique. A variable's coordinate system is the set of coordinate variables used by the variable. Coordinates that refer to physical space are called spatial coordinates, ones that refer to physical time are called time coordinates, ones that refer to either physical space or time are called spatio\ temporal coordinates.
Make coordinate variables for every dimension possible (except for string length dimensions).
Give each coordinate variable at least unit and long_name attributes to document its meaning.
Use an existing netCDF Convention for your coordinate variables, especially to identify spatio-temporal coordinates.
Use shared dimensions to indicate that two variables use the same coordinates along that dimension. If two variables' dimensions are not related, create separate dimensions for them, even if they happen to have the same length. 
```

## Variable attributes

The CF Conventions provides a complete [list of variable attributes](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#attribute-appendix) it covers.
Here we are covering only the ones we beleive are more critical

```{dropdown} units 
CF -
```

```{dropdown} standard_name 
CF - 
```

```{dropdown} calendar 
CF - 
```

```{dropdown} long_name 
CF - highly reccommended 
long_name is not standardes, so it it not used by software. Nonetheless it is very useful has provides a chance to give a more complete description of the variable, highlighting aspect that cannot be specified in other attributes.
For example if the variable is adimensional: percentage, 0-1, etc then the official units is "1". You can then specify what kind of adimensional units in the long_name. 
It is also essential if a standard_name is not available. standard_name are generic, usually they are not sufficient to describe fully a variable.
```

```{dropdown} missing_value 
CF -
```

```{dropdown} cell_methods 
CF -
```
