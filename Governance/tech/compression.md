# NetCDF compression 

## Compression

The netCDF4 format also introduced the ability of adding internal compression to the files. 

### Why compress netCDF files?

**Saving storage**<br>

Compressing netCDF data files can shrink them to one third of their original size. This is the equivalent of being given three times as much disk space.

**NetCDF compression is lossless**<br>

The data is exactly as it was when read from disk. It can still be read using the same programming interface. As long as the program reading the data has been compiled with the latest netCDF library (version 4) then the task of decompressing the data is handled by the library and as far as the programs are concerned there is no difference in the data. The usual tools, such as ncdump, can be used to examine the variables contained within the netCDF file.

```{note}
Compression with tools such as gzip is possible but is not recommended except for archival purposes. It has the disadvantage that the file must be decompressed to be read and then recompressed again when finished, which can be time consuming, not to mention the data in question will take up much more room while it is being analysed.
```

### How does it work?
The netCDF library has several options for compressing data, which all compression programs will use, as they all use the underlying library to perform the compression.

**Deflate level**

This is an integer value from ranging from 0 to 9. A value of 0 means no compression, and 9 is the highest level of compression possible. The higher this value the smaller a file will be once compressed. However, there is a trade-off, the higher the deflate level, the longer it will take to compress, particularly so with very high deflate levels. At deflate level 9 it can take six times longer to compress the data, with only a few percent improvement in compression. The recommended deflate level is 5. This combines good compression with a small increase in compression time.

**Shuffle**

If the `shuffle` option isn't turned on each variable is stored on value, i.e. contiguously in memory. When `shuffle` is turned on, the first bit of all variables is stored contiguously in space, followed by the second bit, and so on.
If the numbers we are storing are similar in values there is a high chance that all the first bits are either all `0` or all `1`, so shuffling produces very long sequences of the same number to store in memory which is very efficient. the same would be true for most of the other bits after the first.
The only case in which shuffling is not a good idea is if neighbouring values differ considerably. Usually turning `shuffle` on results in a smaller compressed file with little performance overhead.

**chunking**
`chunking` also plays a part in the compression process, in order to use netCDF compression the data must be chunked. Without `chunking` a n-dimensional array representing a variable is stored contiguosly in memory, following the dimension order. Using `chunking` an array is broken in units called `chunks`. Each chunk is stored contiguosly in memory, as if it was a separate array. 
There are several chunking strategies that can be applied, mostly depending on how the data is most frequently accessed. Many tools just adopt the netCDF library default chunking strategy. For many netCDF versions the default strategy has been to create chunks that are simply the same size as the grid dimensions of the variable and using size 1 for `time` when present. The [ACDG guide to BigData](https://acdguide.github.io/BigData/data/data-netcdf.html#what-is-data-chunking) covers the implications of different `chunking` strategies on data analysis. 

````{warning}
If dealing with a file with contiguous storage, it is necessary to first chunk the file and then apply compression. Otherwise the compression operation will fail.
The error message will vary depending on the tool used, for example with nccopy
`NetCDF: Bad chunk sizes.`
```{code}
cdo -f nc4 -z zip_5 input-file output-file
```
might work as cdo will impose chunking before compressing.
Another way around this is to use xarray to rewrite the file with the desire encoding, getting a better control of chunking and compression at the same time.
````

```{note}
This [post](https://earthscience.stackexchange.com/questions/12527/regarding-compression-shuffle-filter-of-netcdf4) has a clear representation of how `shuffle` and `chunking` work.
```
## Compression tools

There are several tools that can be used to compress netCDF data, and compression can also be added when creating a file, using the interfaces to the netCDF library available for common programming languages like Python, fortran and MatLab.

**nccopy**

One of the standard tools included in a netCDF installation is [nccopy](https://docs.unidata.ucar.edu/nug/current/netcdf_utilities_guide.html#guide_nccopy). `nccopy` can compress files and define the chunking using a command line argument (-c). `nccopy` is a good option if a data file structure changes little, so a chunking scheme can be decided upon and hard coded into scripts. It is not so useful if the dimensions and variables change. Another major limitation is that the chunking is defined by dimensions, not variables. If a data file has variables that share dimensions, but have different combinations or numbers of dimensions it is not possible to determine an optimal chunking strategy for each variable.

```{code}
nccopy -k nc4 -d 5 -s input.nc output.nc 
```

**NCO**

The [NetCDF Operator](http://nco.sourceforge.net/nco.html#Compression) program suite can compress netCDF files and offers several [chunking strategies](http://nco.sourceforge.net/nco.html#Chunking). 
THis lossless compression is refer to as `deflate` and is usually applied with `shuffle`. The latest versions allows to choose in which order these two operations happen.

```{code}
ncks -D 5 input.nc output.nc
```

NCO also offers three lossy compression algorithms, that can be used in con junction with `deflate`:
* Linear packing - a higher precision type is "packed" into a lower precision type, usually NC_SHORT
And two Precision Preserving Compression (PPC) algorythms where a per-variable precision level is set as:
* Number of Signifcant Digits (NSD) after the decimal point
* Decimal Significant Digits (DSD) before and after the decimal point
For more details refer to the NCO documentation listed above.

**CDO**

[Climate Data Operators](https://code.mpimet.mpg.de/projects/cdo/embedded/index.html#x1-70001.2.1) can also compress netCDF, `shuffle` is automatically enabled and it offers limited chunking options: auto (default), grid or lines.

```{code}
cdo -f nc4 -z zip_5 {-k grid} copy inpput.nc output.nc
```

**nccompress**

The `nccompress` package is available at NCI, as part of the CLEX-CMS conda environment. At present it consists of four python-based programs: `ncfind`, `nc2nc`, `nccompress` and `ncvarinfo`. `nccompress` can copy netCDF files with compression and an optimised chunking strategy that has reasonable performance for many datasets. Its two main limitations: it is slower than the other programs, and it can only compress netCDF3 or netCDF4 classic format.
The `ncfind` utility is used to find netCDF files and discriminate between compressed and uncompressed ones.
For more information refer to the [original documentation](http://climate-cms.wikis.unsw.edu.au/NetCDF_Compression_Tools#General_guidelines)

## Compression by Gathering

This method is described in the CF conventions document:

https://cfconventions.org/Data/cf-conventions/cf-conventions-1.10/cf-conventions.html#_reduction_of_dataset_size

```{admonition} **xbitinfo**
[`xbitinfo`](https://xbitinfo.readthedocs.io/en/latest/) is an xarray-wrapper around [BitInformation.jl](https://github.com/milankl/BitInformation.jl) to retrieve and apply bitrounding from within python. It performs bitwise information analysis and manipulation so that data can be rounded efficiently based on actual information content.
```
