# NetCDF chunking and compression 

## Compression

The NetCDF4 format also introduced the ability of adding internal compression to the files. 

### Why compress NetCDF files?

**Saving storage**<br>
  Data if often stored on a shared filesystem, so it is each user's responsibility to manage the available storage efficiently. Compressing NetCDF data files can shrink them to one third of their original size. This is the equivalent of being given three times as much disk space.

**NetCDF compression is lossless**<br>
 The data is exactly as it was when read from disk. It can still be read using the same programming interface. As long as the program reading the data has been compiled with the latest NetCDF library (version 4) then the task of decompressing the data is handled by the library and as far as the programs are concerned there is no difference in the data. The usual tools, such as ncdump, can be used to examine the variables contained within the NetCDF file.

Compression with tools such as gzip is possible but is not recommended except for archival purposes. It has the disadvantage that the file must be decompressed to be read and then recompressed again when finished, which can be time consuming, not to mention the data in question will take up much more room while it is being analysed.

### How does it work?
The NetCDF library has several options for compressing data, which all compression programs will use, as they all use the underlying library to perform the compression. There is a more detailed explanation if you wish to understand more, but briefly:

**Deflate level**

This is an integer value from ranging from 0 to 9. A value of 0 means no compression, and 9 is the highest level of compression possible. The higher this value the smaller your file will be once compressed. However, there is a trade-off, the higher the deflate level, the longer it will take to compress, particularly so with very high deflate levels. At deflate level 9 it can take six times longer to compress the data, with only a few percent improvement in compression. The recommended deflate level is 5. This combines good compression with a small increase in compression time.

**Shuffle**

Turn shuffle on. Simple. It usually results in a smaller compressed file with little performance overhead.

Finally `chunking` also plays a part in the compression process, in order to use NetCDF compression the data must be chunked. Many tools just adopt the NetCDF library default chunking strategy. For many NetCDF versions the default strategy has been to create chunks that are simply the same size as the grid dimensions of the variable and using size 1 for `time` when present. This can be a disastrous choice in terms of performance if the data is also compressed, as the entire variable/grid must be read into memory to be uncompressed even if only a single slice is required.

```{warning}
COMMENT: to be fixed!!!
If dealing with a file with contiguous storage, it is necessary to first chunk the file and then apply compression. Otherwise the compression operation will fail.
The error messag ewill vary depending on the tool used, for example with nccopy
`NetCDF: Bad chunk sizes.`
cdo -f nc4 -z zip_5 input-file output-file  might work as cdo will impose chunking before compressing
Another way around this is to use xarry to rewrite the file with the desire encoding, getting a better control of chunking and compression at the same time
```

## Compression tools

There are several tools that can be used to compress NetCDF data, and compression can also be added when creating a fileusing the interfaces to the NetCDF library available for common programming languages like Python, fortran and MatLab.

**nccopy**

One of the standard tools included in a NetCDF installation is [nccopy](https://docs.unidata.ucar.edu/nug/current/netcdf_utilities_guide.html#guide_nccopy). `nccopy` can compress files and define the chunking using a command line argument (-c). nccopy is a good option if your data file structure changes little, so a chunking scheme can be decided upon and hard coded into scripts. It is not so useful if the dimensions and variables change. Another major limitation is that the chunking is defined by dimensions, not variables. If your data file has variables that share dimensions, but have different combinations or numbers of dimensions it is not possible to determine an optimal chunking strategy for each variable.

```{code}
nccopy -k nc4 -d 5 -s input.nc output.nc 
```
**NCO**

The [NetCDF Operator](http://nco.sourceforge.net/nco.html#Compression) program suite can compress NetCDF files and has recently included the option to choose different [chunking strategies](http://nco.sourceforge.net/nco.html#Chunking). NCO provides lots of strategies for both chunking and compressing, refer to their doucmentation for more details. 
COMMENT this might not be anymore the case!!!
However, it is not possible to use their optimised chunking strategy for variables with four dimensions or more.

```{code}
ncks -D 5 input.nc output.nc
```

**CDO**

[Climate Data Operators](https://code.mpimet.mpg.de/projects/cdo/embedded/index.html#x1-70001.2.1) can also compress NetCDF, `shuffle` is automatically enabled and it offers limited chunking options: auto (default), grid or lines.

```{code}
cdo -f nc4 -z zip_5 {-k grid} copy inpput.nc output.nc
```

**nccompress**

The `nccompress` package is available at NCI, as part of the CLEX-CMS conda environment. At present it consists of four python-based programs: `ncfind`, `nc2nc`, `nccompress` and `ncvarinfo`. nccompress can copy NetCDF files with compression and an optimised chunking strategy that has reasonable performance for many datasets. Its two main limitations: it is slower than the other programs, and it can only compress NetCDF3 or NetCDF4 classic format. There is more detail in the following sections.
The `ncfind` utility is used to find NetCDF files and discriminate between compressed and uncompressed ones.
For more information refer to the [original documentation](http://climate-cms.wikis.unsw.edu.au/NetCDF_Compression_Tools#General_guidelines)




