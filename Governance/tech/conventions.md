# Applying conventions to your files


## Naming conventions



## Coordinate system

```{dropdown} coordinate variable
A coordinate variable is a one-dimensional variable with the same name as a dimension, which names the coordinate values of the dimension. It must not have any missing data (for example, no _FillValue or missing_value attributes) and must be strictly monotonic (values increasing or decreasing). A two-dimensional variable of type char is a string-valued coordinate variable if it has the same name as its first dimension, e.g.: char time( time, time_len); all of its strings must be unique. A variable's coordinate system is the set of coordinate variables used by the variable. Coordinates that refer to physical space are called spatial coordinates, ones that refer to physical time are called time coordinates, ones that refer to either physical space or time are called spatio\ temporal coordinates.
Make coordinate variables for every dimension possible (except for string length dimensions).
Give each coordinate variable at least unit and long_name attributes to document its meaning.
Use an existing netCDF Convention for your coordinate variables, especially to identify spatio-temporal coordinates.
Use shared dimensions to indicate that two variables use the same coordinates along that dimension. If two variables' dimensions are not related, create separate dimensions for them, even if they happen to have the same length. 
```

Requirements:

The time units of a time coordinate variable must contain a reference time.

The reference time of a time coordinate variable must be a legal time in the specified calendar.

Recommendations:

The use of a reference time in the year 0 to indicate climatological time is deprecated. This restriction only applies to the real-world calendar as used by the udunits package.

Units of year and month and any equivalent units should be used with caution.

Cliamtological statistics (check document)

```{dropdown} calendar 
CF - recommended
the [calendar](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#calendar) attribute defines the calendar used by the time coordinate. In order to calculate a time coordinate value from a date/time, or the reverse, one must know the units attribute of the time coordinate variable (containing the time unit of the coordinate values and the reference date/time) and the calendar. The choice of calendar defines the set of dates (year-month-day combinations) which are permitted, and therefore it specifies the number of days between the times of 0:0:0 (midnight) on any two dates. Date/times which are not permitted in a given calendar are prohibited in both the encoded time coordinate values, and in the reference date/time string. It is recommended that the calendar be specified by the calendar attribute of the time coordinate variable. 
```

## Variable attributes

The CF Conventions provides a complete [list of variable attributes](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#attribute-appendix) it covers.
Here we are covering only the ones we believe are more critical. It is also worth to point out that lots of these attributes are not required but highly recommended for backwards compatibility with COARDS. However, they are usually expected for the files to be considered CF compliants, whenever they are applicable.

```{dropdown} units 
CF - required
Latitude, longitude, and time coordinates are identified solely by the value of their units attribute. Vertical coordinates with units of pressure may also be identified by the units attribute. Other vertical coordinates must use the attribute positive which determines whether the direction of increasing coordinate value is up or down. Because identification of a coordinate type by its units involves the use of an external software package [UDUNITS](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#UDUNITS), we provide the optional attribute axis for a direct identification of coordinates that correspond to latitude, longitude, vertical, or time axes.
```

```{dropdown} long_name 
CF - highly recommended 
the [long_name](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#long-name) attribute provides a description of the variable. Either long_name or standard_name are expected to be present, ideally they both are. Standard_names are designed tcribed only a physical quantity, as air_temperature, this is usually not sufficient on its own to describe fully a variable.
Long_name provides a chance to give a more complete description of the variable, highlighting aspect that cannot be specified in other attributes.
For example if the variable is adimensional: percentage, 0-1, etc then the official units is "1". You can then specify what kind of adimensional units in the long_name. 
Long_name is also often used to label plots.
```

```{dropdown} standard_name 
CF - highly  recommended
The [standard_name](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#standard-name) attribute is used to identify the variable content. A list of the approved standard_names is available [here](http://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html). The variable needs to have units which are physically equivalent, if not the same, as the ones listed to be able to use a standard_name. A standard name contains no whitespace, underscores are used instead, and is case sensitive. The variable definition can be further clarified using [modifiers](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#standard-name-modifiers), modifications due to common statistical operations are expressed via the cell_methods attribute. Even so, not all variables can be mapped to a standard_name, while this is a required attribute for the CF conventions, it should be left out if not existing. Empty string are not valid. It was introduced to provide an objective definition of a variable. The long_name attribute was, and still is, useful to provide a description of the variable, but as it is defined ad hoc by the dataset creator it is not possible to use it programatically to individuate a specific variable, across different files. For example, standard_names can be used by online data catalogues to query all datasets that provide a particular variable.   
```

```{dropdown} cell_methods 
CF -
```

```{dropdown} missing and valid data related 
CF -
_FillValue, missing_value, valid_min, valid_max, and valid_range attributes to indicate missing data. Missing data is allowed in data variables and auxiliary coordinate variables. Generic applications should treat the data as missing where any auxiliary coordinate variables have missing values; special-purpose applications might be able to make use of the data. Missing data is not allowed in coordinate variables.
```

```{dropdown} ancillary data
CF -
```

```{dropdown} coverage_content_type
ACDD - highly recommended 
```

Important link:
https://cfconventions.org/Data/cf-documents/requirements-recommendations/conformance-1.8.html

exceptions for boundary and climatology variables

The units level, layer, and sigma_level are deprecated.

## Global attributes
Global attributes are the ones that apply to the entire file. Global attributes are useful to record provenance: keep track of operations applied to the file, data sources and software used to generate the data, any party involved. They are also used at publication stage when conventions like ACDD build on the CF ones to add publication related information, as DOI, contact, license and references. 
While global attributes are the most useful when sharing data, for example to increase discoverability, using some key ones from the start of the file creation is important to keep track of the file history. Often this level of information is neglected when saving data to a file, which can make it hard if not impossible reconstruct the analysis workflow later on with some certainty. Also, as global attributes are preserved during most of analysis operations, output files end up containing a legacy of global attributes from the source file which is usually not anymore relevant to the new data.
Institution, source, references, and comment can also be assigned to individual variables, in such case the variable version has precedence.

```{dropdown} Conventions 
CF - required
This attribute simply indicates the conventions applied to the file, as such is one of the few required attributes, as it provides the key to correctly interpret all the other attributes. For CF conventions the expected value is `CF-<version>` for example `CF-1.8`. if more than a convention is applied to the file then they should be provided as a list separated by blank spaces or commas.
```

```{dropdown} title 
CF - highly recommended
```

```{dropdown} institution 
CF - highly recommended
```

```{dropdown} source 
CF - highly recommended
This attribute indicates the method of production of the original data. It should be as detailed as possible so, for example, if the data is model generated also the version and if applicable details of configuration used should be present. It's often easier if the source of the data is complex to use a link to documentation. While this attributes definition focuses on the `method of production`, often source is also used to list the input data, this is because data is actually the product of analysis performed on an existing dataset. In such a case can also be handy to preserve some of the dataset original global attributes but prefacing them with `source_`, for example `source_license`. Alternatively, as a specific attribute for input data does not exist in conventions, `source_data`, `input`, `input_data`, are often used. CMIP conventions uses `parent_` to indicate properties of parent experiments used to initialise model simulations.   
```

```{dropdown} history 
CF - highly recommended
```

```{dropdown} references 
CF - highly recommended
```

```{dropdown} comment 
CF - highly recommended
this can also be used at variable level
```

```{dropdown} summary 
ACDD - highly recommended
```

```{dropdown} keywords
ACDD - highly recommended
```

```{dropdown} id 
ACDD - recommended
```

```{dropdown} license 
ACDD - recommended
```

```{dropdown}  creator_(name/email/url) 
ACDD - recommended
```

```{dropdown} geospatial_<>/time_coverage_<> 
ACDD - recommended
```

```{dropdown} created_date 
ACDD - recommended
```

