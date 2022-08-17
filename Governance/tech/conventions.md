# Applying conventions to your files


## Naming conventions


useful summary: https://cfconventions.org/Data/cf-documents/requirements-recommendations/conformance-1.9.html

NetCDF files are required to have the file name extension ".nc".

There are no recognised naming conventions for variable names, but CMIP projects created their own [naming convention]() and this is often used althought it is not recognised as official outside the ESGF projects.
The iuse of the standard_name attribute described below is an attempt to remediate to this and make it easier for software developer to identify and treat in a special way dimensions and other common variables.

It is required that CF attributes that take string values must be 1D character arrays or single atomic strings.
Requirements:

The external_variables attribute is of string type and contains a blank-separated list of variable names.

No variable named by external_variables is allowed in the file.

Recommendations:

Variable, dimension and attribute names should begin with a letter and be composed of letters, digits, and underscores.

No two variable names should be identical when case is ignored.

Requirements:

The dimensions of a variable must all have different names.

Recommendations:

If any or all of the dimensions of a variable have the interpretations (as given by their units or axis attribute) of time (T), height or depth (Z), latitude (Y), or longitude (X) then those dimensions should appear in the relative order T, then Z, then Y, then X in the CDL definition corresponding to the file.

In files that are meant to conform to the COARDS subset of CF, any dimensions of a variable other than space and time dimensions should be added "to the left" of the space and time dimensions as represented in CDL.


````{warning}
Attribute names commencing with underscore ('_') are reserved for use by the netCDF library.
````

## Coordinate system

```{dropdown} **coordinate variable**
A coordinate variable is a one-dimensional variable with the same name as a dimension, which names the coordinate values of the dimension.
* It must not have any missing data (for example, no _FillValue or missing_value attributes) and must be strictly monotonic (values increasing or decreasing). 
* A two-dimensional variable of type char is a string-valued coordinate variable if it has the same name as its first dimension, e.g.: char time( time, time_len); all of its strings must be unique. A variable's coordinate system is the set of coordinate variables used by the variable. Coordinates that refer to physical space are called spatial coordinates, ones that refer to physical time are called time coordinates, ones that refer to either physical space or time are called spatio\ temporal coordinates.
* Make coordinate variables for every dimension possible (except for string length dimensions).
* Give each coordinate variable at least unit and long_name attributes to document its meaning.
* Use an existing NetCDF Convention for your coordinate variables, especially to identify spatio-temporal coordinates.
* Use shared dimensions to indicate that two variables use the same coordinates along that dimension. If two variables' dimensions are not related, create separate dimensions for them, even if they happen to have the same length. 
```

!!! other type of cocrdinates!!!
scalar coordinate variable
A scalar variable (i.e. one with no dimensions) that contains coordinate data. Depending on context, it may be functionally equivalent either to a size-one coordinate variable (Section 5.7, "Scalar Coordinate Variables") or to a size-one auxiliary coordinate variable (Section 6.1, "Labels" and Section 9.2, "Collections, instances, and elements").


**Requirements**

* The time units of a time coordinate variable must contain a reference time.
* The reference time of a time coordinate variable must be a legal time in the specified calendar.

**Recommendations**

* The use of a reference time in the year 0 to indicate climatological time is deprecated. This restriction only applies to the real-world calendar as used by the udunits package. For more information on how to describe climatological statistics refer to the [CF documentation](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#climatological-statistics).

* Units of year and month and any equivalent units should be used with caution.

```{dropdown} **calendar** 
**CF - recommended**<br>
The [calendar](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#calendar) attribute defines the calendar used by the time coordinate. In order to calculate a time coordinate value from a date/time, or the reverse, one must know the units attribute of the time coordinate variable (containing the time unit of the coordinate values and the reference date/time) and the calendar.<br>
The choice of calendar defines the set of dates (year-month-day combinations) which are permitted, and therefore it specifies the number of days between the times of 0:0:0 (midnight) on any two dates. Date/times which are not permitted in a given calendar are prohibited in both the encoded time coordinate values, and in the reference date/time string.
<br>It is recommended that the calendar be specified by the calendar attribute of the time coordinate variable. 
```

## Variable attributes

The CF Conventions provides a complete [list of variable attributes](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#attribute-appendix) it covers.<br>
Here we are covering only the ones we believe are more critical. It is also worth to point out that only a few attributes are `required` to maintain backwards compatibility with COARDS. However, most of the `highly recommended` ones are expected for the files to be considered CF compliant, whenever they are applicable.

```{dropdown} **units** 
**CF - required**<br>
It is important to use the correct units are software often uses them without the users being aware of it.<br>
This is especially true for dimensions as latitude, longitude, and time coordinates are identified solely by the value of their units attribute. Vertical coordinates with units of pressure may also be identified by the units attribute. Other vertical coordinates must use the attribute positive which determines whether the direction of increasing coordinate value is up or down. <br>
Because identification of a coordinate type by its units involves the use of an external software package [UDUNITS](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#UDUNITS), only exceptions are the units for level, layer, and sigma_level.<br>
CF provides the optional attribute axis for a direct identification of coordinates that correspond to latitude, longitude, vertical, or time axes.<br>
If the variable is adimensional: percentage, 0-1, etc then the official units is always "1".
```

```{dropdown} **long_name** 
**CF - highly recommended**<br> 
The [long_name](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#long-name) attribute provides a description of the variable. Either long_name or standard_name is expected to be present ideally, they both are.<br>
Standard_names are designed to described the physical quantity, as air_temperature, this is usually not sufficient on its own to describe fully a variable.<br>
Long_name provides a chance to give a more complete description of the variable, highlighting aspects that cannot be specified in other attributes.
For example, adimensional variables have "1" as units. Long_name can be used to specify what kind of adimensional units: percentage, 0-1, ppm etc.<br>
Long_name is also often used to label plots.
```

```{dropdown} **standard_name** 
**CF - highly  recommended**<br>
The [standard_name](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#standard-name) attribute is used to identify the variable content. A list of the approved standard_names is available [here](http://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html).<br>
It was introduced to provide an objective definition of a variable. The long_name attribute was, and still is, useful to provide a description of the variable, but as it is defined ad hoc by the dataset creator it is not possible to use it programmatically to individuate a specific variable, across different files. For example, standard_names can be used by online data catalogues to query all datasets that provide a particular variable.<br>
The variable needs to have units which are physically equivalent, if not the same, as the ones listed to be able to use a standard_name. A standard name contains no whitespace, underscores are used instead, and is case sensitive.<br>
The variable definition can be further clarified using [modifiers](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#standard-name-modifiers), modifications due to common statistical operations are expressed via the cell_methods attribute.<br>
If a variable has a standard_name of region or area_type, it must have value(s) from the permitted lists: [region list](https://cfconventions.org/Data/standardized-region-list/standardized-region-list.html) and [area_type list](http://cfconventions.org/Data/area-type-table/current/build/area-type-table.html).

````{warning}
Even so, not all variables can be mapped to a standard_name, while this is a required attribute for the CF conventions, it should be left out if not existing. Empty strings are not valid.
````
```

```{dropdown} **cell_methods** 
CF -
```

```{dropdown} **missing and valid data** 
CF -
`_FillValue`, `missing_value`, `valid_min`, `valid_max`, and `valid_range` attributes are used to indicate missing data. Missing data is allowed in data variables and auxiliary coordinate variables. Generic applications should treat the data as missing where any auxiliary coordinate variables have missing values; special-purpose applications might be able to make use of the data.<br>
Missing data is not allowed in coordinate variables.
The [_FillValue](https://docs.unidata.ucar.edu/netcdf-c/current/attribute_conventions.html#autotoc_md89) attribute specifies the fill value used to pre-fill disk space allocated to the variable, it is then returned when reading values which were never written. 
If _FillValue is defined then it should be scalar and of the same type as the variable. If the variable is packed using scale_factor and add_offset attributes, the _FillValue attribute should have the data type of the packed data.<br>
If not defined the deafult fill value for the type of the variable is used. However, use of the default fill value for data type byte is not recommended.<br>
Note that changing the value of this attibute, won't changed previously 'filled' data automatically.<br>
If valid_range is specified _FillValue should be outside of this range.

The `missing_value` is not treated in any special way by the NetCDF library, but it may be used by specific applications. The missing_value attribute can be a scalar or vector containing values indicating missing data. These values should all be outside the valid range.<br>
When scale_factor and add_offset are used, the value(s) of the missing_value attribute should be specified in relation to the packed data, so that missing values can be detected before the scale_factor and add_offset are applied.<br>
If both missing_value and _FillValue are used, they should have the same value.

The `actual_range` defines a two-element vector for numeric variables, composed of the exact minimum and the maximum data values and both must be within the valid_range if specified.<br>
If the variable is packed, the elements of the actual_range should be defined based on the unpacked data, including the type.<br>
If the data is all missing or invalid, the actual_range attribute cannot be used.

The 'valid_range` attribute is mutually exclusive with `valid_min` and `valid_max` attributes. If none of them is defined software applications will use _Fill_value and the variable type to try to determine a valid range.
```

```{dropdown} **ancillary data**
CF -
```

```{dropdown} **coverage_content_type**
ACDD - highly recommended 
```

````{warning}
In xarray variable attributes are kept across operations depending on the value of the `keep_attrs` argument. Its default behaviour is to keep them in unambiguous circumstances. If set to True it will always keep the attributes, if set to False it will discard them.<br>
It is important to be aware of this, as particularly for coordinates, units and cell_methods are easily changed by calculations and often inherited attributes become meaningless or worst can cause issues if not updated. The same can also happen with other softwares.
````

Important link:
https://cfconventions.org/Data/cf-documents/requirements-recommendations/conformance-1.8.html

exceptions for boundary and climatology variables

The units level, layer, and sigma_level are deprecated.

## Global attributes
Global attributes are the ones that apply to the entire file. Global attributes are useful to record provenance: keep track of operations applied to the file, data sources and software used to generate the data, any party involved. They are also used at publication stage when conventions like ACDD build on the CF ones to add publication related information, as DOI, contact, license and references. 
While global attributes are the most useful when sharing data, for example to increase discoverability, using some key ones from the start of the file creation is important to keep track of the file history. Often this level of information is neglected when saving data to a file, which can make it hard if not impossible reconstruct the analysis workflow later on with some certainty. Also, as global attributes are preserved during most of analysis operations, output files end up containing a legacy of global attributes from the source file which is usually not anymore relevant to the new data.
Institution, source, references, and comment can also be assigned to individual variables, in such case the variable version has precedence.

Requirements:

The title, history, institution, source, references, and comment attributes are all type string.

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

