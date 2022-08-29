# Writing valid and compliant netCDF files

This page covers the basic netCDF structure and the application of the CF and ACDD conventions to netCDF files. Not all the rules are listed here, this is just a summary of the most common ones, for a complete overview of both conventions refer to their official documentation (see references).
This summary is meant to help setting variables and attributes correctly at file creation, for existing files a CF checker tool can be used. We cover some available tools in the [next page](cf-checker.md).

```{warning}
While CF checkers programs are useful for a quick assessment of a file, it is important to remember that:
* None of them can check all the requirements and recommendations, they might miss rules for attributes which are used less often or ones that are too complex to code.
* A file might satisfy all the rules but have incorrect information, i.e., all variables have units defined, but some of them are incorrect
```

## Naming conventions

There are no recognised vocabularies for files and variable names, however the ESGF created their own [variable definition tables](https://github.com/PCMDI/cmip6-cmor-tables/tree/master/Tables) for the CMIP output and this is often used by other projects.
The CF conventions only have some basic requirements and recommendations on how to form the names. 

**Requirements**

* NetCDF files are required to have the file name extension `.nc`.
* The dimensions of a variable must all have different names.
* If the `external_variables` attribute is used, variables with the same names are not allowed in the file.

**Recommendations**

* Variable, dimension and attribute names should begin with a letter and be composed of letters, digits, and underscores.
* No two variable names should be identical when case is ignored.


Requirements:

The external_variables attribute is of string type and contains a blank-separated list of variable names.


````{warning}
Attribute names commencing with underscore ('_') are reserved for use by the netCDF library.
````

## Coordinate system
A coordinate system is described in netCDF files through the combinations of its dimensions, coordinates and projections.
A `coordinate variable` is a one-dimensional variable representing a dimension and sharing its name. An `auxiliary coordinate variable` is an additional or alternative coordinate for an axis. Finally a `scalar coordinate variable` is a coordinate with no dimension (i.e., of size one). 

```{dropdown} **dimension**
A dimension has both a name and a length, which is an arbitrary positive integer. The special value of `UNLIMITED` indicates an unlimited or record dimension. A variable with an unlimited dimension can grow to any length along that dimension.<br>
A netCDF classic dataset can have at most one unlimited dimension, if present this must be the most significant (slowest changing) one and so also the first dimension in a CDL or other array declarations.<br>
A netCDF-4 file may have multiple unlimited dimensions, and there are no restrictions on their order.
```

```{dropdown} **coordinate variable**
A coordinate variable is a one-dimensional variable with the same name as a dimension, which names the coordinate values of the dimension.
* It must not have any missing data (for example, no _FillValue or missing_value attributes) and must be strictly monotonic (values increasing or decreasing). 
* A two-dimensional variable of type char is a string-valued coordinate variable if it has the same name as its first dimension, e.g.: char time( time, time_len); all of its strings must be unique.
* Make coordinate variables for every dimension possible (except for string length dimensions).
* Give each coordinate variable at least unit and long_name attributes to document its meaning.
* Use an existing netCDF Convention for your coordinate variables, especially to identify spatio-temporal coordinates.
* Use shared dimensions to indicate that two variables use the same coordinates along that dimension. If two variables' dimensions are not related, create separate dimensions for them, even if they happen to have the same length. 
```

The most common dimensions and coordinates are `time`, `latitude`, `longitude` and the vertical coordinate (`depth` or `height`). These have a special attribute `axis`:  

**Requirements**

* The only legal values of axis are `X`, `Y`, `Z`, and `T` (case insensitive).
* The only legal values for the `positive` attribute, assciated with the Z axis, are `up` or `down` (case insensitive).
* The axis attribute must be consistent with the coordinate type deduced from the attributes `units` and `positive`.
* The axis attribute is not allowed for auxiliary coordinate variables.
* A data variable must not have more than one coordinate variable with a particular value of the axis attribute.

**Recommendations**

* If any or all of the dimensions of a variable have the interpretations (as given by their units or axis attribute) of time (T), height or depth (Z), latitude (Y), or longitude (X) then those dimensions should appear in the relative order T, then Z, then Y, then X in the CDL definition corresponding to the file.
* Any dimensions of a variable other than space and time dimensions should be added "to the left" of the space and time dimensions as represented in CDL.

### Time coordinate

The time coordinate is well defined by the `units` and the `calendar` attributes. The standard time definition doesn't work for climatological statistics, as a calendar year, month and day of the year are not well defined units of time and they usually change depending on the calendar. For more information on how to describe climatological statistics refer to the [CF documentation](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#climatological-statistics).

**Requirements**
* The time units of a time coordinate variable must contain a reference time.
* The reference time of a time coordinate variable must be a legal time in the specified calendar.

**Recommendations**

* A time coordinate variable should have a calendar attribute.
* The use of a reference time in the year 0 to indicate climatological time is deprecated. 
* Year and month should not be used as `units`, because of the potential for mistakes and confusion.

```{warning}
CF standards follows UDUNITS definition of a year to be exactly 365.242198781 days, and a month to be exactly year/12. These are different from a calendar year and a calendar month.
```

```{dropdown} **calendar** 
**CF - recommended**<br>
The [calendar](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#calendar) attribute defines the calendar used by the time coordinate. In order to calculate a time coordinate value from a date/time, or the reverse, one must know the `units` attribute of the time coordinate variable (containing the time unit of the coordinate values and the reference date/time) and the calendar.<br>
The choice of calendar defines the set of dates (year-month-day combinations) which are permitted, and therefore it specifies the number of days between the times of 0:0:0 (midnight) on any two dates. Date/times which are not permitted in a given calendar are prohibited in both the encoded time coordinate values, and in the reference date/time string.<br>

**Requirements**

* The attributes calendar, month_lengths, leap_year, and leap_month may only be attached to time coordinate variables.
* The standardized values (case insensitive) of the calendar attribute are `standard`, `gregorian` (deprecated), `proleptic_gregorian`, `noleap`, `365_day`, `all_leap`, `366_day`, `360_day`, `julian`, and `none`. 
* If the calendar attribute is given a non-standard value, then the attribute `month_lengths` is required, along with `leap_year` and `leap_month` as appropriate.
* The type of the `month_lengths` attribute must be an integer array of size 12.
* The values of the `leap_month` attribute must be an integer in the range 1-12.

**Recommendations**

* The value `standard` should be used instead of `gregorian` in the calendar attribute.
* The attribute `leap_month` should not appear unless the attribute `leap_year` is present.
* The time coordinate should not cross the date 1582-10-15 when the default mixed Gregorian/Julian calendar is in use.
```

## Variable attributes

The CF Conventions provides a complete [list of variable attributes](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#attribute-appendix) it covers.<br>
Here we are covering only the ones we believe are more critical. It is also worth to point out that only a few attributes are `required` to maintain backwards compatibility with COARDS. However, most of the `highly recommended` ones are expected for the files to be considered CF compliant, whenever they are applicable.

````{dropdown} **units** 
**CF - required**<br>
The attribute [`units`](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#units) is essential for all variables representing dimensional quantities.
This is especially true for dimensions as latitude, longitude, and time coordinates which the netCDF library identifies solely by the value of their `units` attribute. This identification uses the [UDUNITS package](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#UDUNITS).<br> 
Vertical coordinates with units of pressure may also be identified by the `units` attribute. Other vertical coordinates must use the attribute positive which determines whether the direction of increasing coordinate value is `up` or `down`. <br>
CF provides the optional attribute `axis` for a direct identification of coordinates that correspond to latitude, longitude, vertical, or time axes.<br>

**Requirements**
* The value of the `units` attribute is a string from the UDUNITS library
* If the variable is adimensional: percentage, 0-1, etc then the official value for `units` is always `1`.

**Recommendations**
* The units `level`, `layer`, and `sigma_level` are allowed for backwards compatibility with COARDS but they are deprecated and shouldn't be used for new files, as dimensionless vertical coordinates do not require a `units` attribute.

```{admonition} Tip
NCICS provides an online [UDUNITS2 database](https://ncics.org/portfolio/other-resources/udunits2/) including full list of all units and prefixes by name and symbol. 
```
````

```{dropdown} **long_name** 
**CF - highly recommended**<br> 
The [long_name](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#long-name) attribute provides a description of the variable. Either long_name or standard_name is expected to be present ideally, they both are.<br>
Standard_names are designed to describe the physical quantity, as air_temperature, this is usually not sufficient on its own to describe fully a variable.<br>
Long_name provides a chance to give a more complete description of the variable, highlighting aspects that cannot be specified in other attributes.
For example, adimensional variables have `1` as units. Long_name can be used to specify what kind of adimensional units: percentage, 0-1, ppm etc.<br>
Long_name is also often used to label plots.
```

````{dropdown} **standard_name** 
**CF - highly  recommended**<br>
The [`standard_name`](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#standard-name) attribute is used to identify the variable content. A list of the approved standard_names is available [here](http://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html).<br>
It was introduced to provide an objective definition of a variable. The `long_name` attribute was, and still is, useful to provide a description of the variable, but as it is defined ad hoc by the dataset creator it is not possible to use it programmatically to individuate a specific variable, across different files. For example, `standard_name` can be used by online data catalogues to query all datasets that provide a particular variable.<br>

**Requirements**<br>
* `standard_name` contains no whitespace, underscores are used instead, and is case sensitive.<br>
* The variable needs to have units which are physically equivalent, if not the same, as the ones listed to be able to use a `standard_name`. 
* If a variable has a standard_name of region or area_type, it must have value(s) from the permitted lists: [region list](https://cfconventions.org/Data/standardized-region-list/standardized-region-list.html) and [area_type list](http://cfconventions.org/Data/area-type-table/current/build/area-type-table.html).

**Recommendations**<br>
* The variable definition can be further clarified using [modifiers](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#standard-name-modifiers), modifications due to common statistical operations are expressed via the cell_methods attribute.<br>

```{warning}
NEVER MAKE UP YOUR OWN STANDARD NAME!!! If it's not defined for your variable you must not use this metadata attribute.
Empty strings are not valid.
```

````

```{dropdown} **cell_methods** 
**CF - recommended**<br>
[`cell_methods`](http://cfconventions.org/cf-conventions/cf-conventions.html#appendix-cell-methods) describes a characteristic (usually statistical) of the cell values. `cell_methods` is useful where a variable could be intepreted both as an extensive (which depends on the size of the cell) or intensive (which does not) quantity.
For example, a precipitation rate could be instantaneous (intensive) or a mean value over the time interval specified by the cell (extensive).<br>

**Requirements**<br>
* It is a string attribute comprising a list of `name: method` pairs, where `name` indicates the dimension or coordinate to which the method is applied. For example, `cell_methods="time: mean"` means that each cell value represents the  time averaged value.
* To list different methods for different axis: `cell_methods="time: mean longitude: max"`.
* The values of method should be selected from [this list](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#appendix-cell-methods).

**Recommendations**<br>
* The word 'area' can also be used as `name` (see [here](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#cell-methods-no-coordinates)).
* To clarify that a cell value is "instantaneous" use `point` as method.
* Every data variable should include for each of its dimensions and each of its scalar coordinate variables the cell_methods information of interest (unless this information would not be meaningful). 
* It is especially recommended that cell_methods be explicitly specified for each spatio-temporal dimension and each spatio-temporal scalar coordinate variable.
```

```{dropdown} **missing and valid data** 
**CF - recommended**<br>
[`_FillValue`, `missing_value`, `valid_min`, `valid_max`, and `valid_range`](https://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html#missing-data) attributes are used to indicate missing data. Missing data is allowed in data variables and auxiliary coordinate variables. Generic applications should treat the data as missing where any auxiliary coordinate variables have missing values; it's very important to define this value so that NaNs are properly interpreted by as many tools as possible.<br>
Missing data is not allowed in coordinate variables.<br>

**_FillValue**<br>
The [`_FillValue`](https://docs.unidata.ucar.edu/netcdf-c/current/attribute_conventions.html#autotoc_md89) attribute specifies the fill value used to pre-fill disk space allocated to the variable, it is then returned when reading values which were never written. 
If `_FillValue` is defined then it should be scalar and of the same type as the variable. If the variable is packed using scale_factor and add_offset attributes, the _FillValue attribute should have the data type of the packed data.<br>
If not defined the deafult fill value for the type of the variable is used. However, use of the default fill value for data type byte is not recommended.<br>
Note that changing the value of this attibute, won't changed previously 'filled' data automatically.<br>
If `valid_range` is specified `_FillValue` should be outside of this range.

**missing-value**<br>
The `missing_value` is not treated in any special way by the netCDF library, but it may be used by specific applications. The missing_value attribute can be a scalar or vector containing values indicating missing data. These values should all be outside the valid range.<br>
When scale_factor and add_offset are used, the value(s) of the missing_value attribute should be specified in relation to the packed data, so that missing values can be detected before the scale_factor and add_offset are applied.<br>
If both missing_value and _FillValue are used, they should have the same value.

**actual_range**<br>
The `actual_range` defines a two-element vector for numeric variables, composed of the exact minimum and the maximum data values and both must be within the valid_range if specified.<br>
If the variable is packed, the elements of the actual_range should be defined based on the unpacked data, including the type.<br>
If the data is all missing or invalid, the actual_range attribute cannot be used.

**valid_range, valid_min, valid_max**<br>
The `valid_range` attribute is mutually exclusive with `valid_min` and `valid_max` attributes. If none of them is defined software applications will use `_FillValue` and the variable type to try to determine a valid range.
```

```{dropdown} **ancillary data**
CF -
```

```{dropdown} **coverage_content_type**
**ACDD - highly recommended** 
```

````{warning}
In xarray variable attributes are kept across operations depending on the value of the `keep_attrs` argument. Its default behaviour is to keep them in unambiguous circumstances. If set to True it will always keep the attributes, if set to False it will discard them.<br>
It is important to be aware of this, as particularly for coordinates, units and cell_methods are easily changed by calculations and often inherited attributes become meaningless or worst can cause issues if not updated. The same can also happen with other softwares.
````

There are various tools available to help you check your files against a version of the CF Conventions. The CLEX CMS covered some on their [wiki](http://climate-cms.wikis.unsw.edu.au/CF_checker).  

## Global attributes
Global attributes are the ones that apply to the entire file. Global attributes are useful to record provenance: keep track of operations applied to the file, data sources and software used to generate the data, any party involved. They are also used at publication stage when conventions like ACDD build on the CF ones to add publication related information, as DOI, contact, license and references.<br>
While global attributes are the most useful when sharing data, for example to increase discoverability, using some key ones from the start of the file creation is important to keep track of the file history. Often this level of information is neglected when saving data to a file, which can make it hard if not impossible to reconstruct the analysis workflow.<br>
Also, as global attributes are preserved during most of analysis operations, output files end up containing information from the source file which is usually not anymore relevant to the new data.<br>
`institution`, `source`, `references`, and `comment` can also be assigned to individual variables, in such case the variable version has precedence.

**Requirements**

The `title`, `history`, `institution`, `source`, `references`, and `comment` attributes are all type string.

```{dropdown} **Conventions** 
**CF - required**
This attribute simply indicates the conventions applied to the file, as such is one of the few required attributes, as it provides the key to correctly interpret all the other attributes. For CF conventions the expected value is `CF-<version>` for example `CF-1.8`. if more than a convention is applied to the file then they should be provided as a list separated by blank spaces or commas.
```

```{dropdown} **title** 
**CF - highly recommended**
```

```{dropdown} **institution** 
**CF - highly recommended**
or only recom???
The name of the institution principally responsible for originating this data.
```

```{dropdown} **source** 
**CF - highly recommended**
**ACDD - recommended**
This attribute indicates the method of production of the original data. It should be as detailed as possible so, for example, if the data is model generated also the version and if applicable details of configuration used should be present. It's often easier if the source of the data is complex to use a link to documentation.<br>
While this attribute's definition focuses on the method, often source is also used to list the input data. If a the file is derived directly form another dataset, it is good practice to preserve some of the dataset original global attributes but prefacing them with `source_`, for example `source_license`. Alternatively, as a specific attribute for input data does not exist in conventions, `source_data`, `input`, `input_data`, are often used. CMIP conventions uses `parent_` to indicate properties of parent experiments used to initialise model simulations.   
```

```{dropdown} **history** 
**CF - highly recommended**
```

```{dropdown} references 
**CF - highly recommended**
```

```{dropdown} **comment** 
**CF - highly recommended**
this can also be used at variable level
```

```{dropdown} **summary** 
**ACDD - highly recommended**
```

```{dropdown} **keywords**
**ACDD - highly recommended**
```

```{dropdown} **id** 
**ACDD - recommended**
```

```{dropdown} **license** 
**ACDD - recommended**
```

```{dropdown}  **creator_(name/ email/ url)** 
**ACDD - recommended**
Respectively, the name, email and a web address (if available) of the person (or other creator type specified by the creator_type attribute) principally responsible for creating this data.
```

```{dropdown}  **publisher_(name/ email/ url)** 
**ACDD - recommended**
The name of the person (or other entity specified by the publisher_type attribute) responsible for publishing the data file or product to users, with its current metadata and format.

```
```{dropdown} **geospatial_<> / time_coverage_<>** 
**ACDD - recommended**
```

```{dropdown} **created_date** 
**ACDD - recommended**
The date on which this version of the data was created.
The ISO 8601:2004 extended date format is recommended add example
```

**References**<br>
A useful summarised version of [requirements and recommendations](https://cfconventions.org/Data/cf-documents/requirements-recommendations/conformance-1.9.html) for CF conventions.

