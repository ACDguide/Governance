# CF compliance checkers

There are a few options when it comes to checking if files are CF compliant. There are online checkers, a netCDF is uploaded and a report to download is generated for the file, examples are:

* https://compliance.ioos.us/index.html

* http://cfconventions.org/compliance-checker.html

This works fine for one small file but when checking a lot of files is better to install and use a checker.<br>
The IOOS checker is recommended for this. If working at NCI, this is already installed in the CLEX managed conda environments.
The IOOS checker is python based, it checks for CF conventions and the ACDD conventions. NCI uses this checker as part of their publishing process, as it covers both CF and ACDD conventions, which are required to publish on their data portal. 

## Running IOOS at NCI
Using it is very simple, just load the conda module

```{code}
$ module use /g/data/hh5/public/modules
$ module load conda/analysis3
```

And call the checker on a netCDF file:

```{code}
$ cchecker.py test_file.nc


Running Compliance Checker on the datasets from: ['test_file.nc']
--------------------------------------------------------------------------------
                        IOOS Compliance Checker Report                         
                                    acdd:1.3                                    
http://wiki.esipfed.org/index.php?title=Category:Attribute_Conventions_Dataset_Discovery
--------------------------------------------------------------------------------
                               Corrective Actions                               
test_file.nc has 4 potential issues
                               Highly Recommended                               
--------------------------------------------------------------------------------
Global Attributes
* Conventions does not contain 'ACDD-1.3'
* summary not present
.........
```

As seen from the example, without passing any option, the tool checks for ACDD 1.3 (the latest version) compliance. The report is printed out to screen.

```{code}
$ cchecker.py --help
```

will list all the available options, the main ones are:

```{code}
 -t/--test  to choose the test;

     ie.e -t=cf  will test the file against the latest available version of the CF conventions.

 -l/--list  to list the available tests.

 -c /-- criteria set the level to which to run the test;

      possible options are < lenient, normal, strict >, default to <normal>

 -f/--format  the output format;

      possible options are < text, html, json, json_new >

 -o/--output optional file/s to redirect output to.

```

### Checking multiple files
You can also run the checker on several files at one time. For example:

```{code}
$ cchecker.py -t=cf -c strict -o cf_test.txt test_data/test*.nc 
```

This example shows how to check all the files matching `test_data/test*.nc` against the CF standards, the standard is applied at a `strict` level and the report is written to the file `cf_test.txt`.

When testing mutiple files, the tools print a report for each file, if there are a lot of files, the report will be long and repetitive.

The CLEX CMS team created a [simple python script](https://gist.github.com/paolap/e37447c9c00e8894437b13a76021c857) that can be run to summarise the report so each error or warning is reported only once.

This script creates a summary of CF/ACDD tests run by the IOOS checker on multiple files

First run the checker generating a json output, for example:

```{code}
$ cchecker.py -t=cf -c strict -f json_new -o cf_test.json test_data/test*.nc  
```

Then pass the json file as input to this script

```{code}
$ python parse_checker.py test.json
```

```{dropdown} Summarised reports
Results for cf checks
3 files were checked

High priority results

3 files failed:
�2.2 Data Types: The variable time failed because the datatype is int64

3 files failed:
�3.3 Standard Name: Attribute long_name or/and standard_name is highly recommended for variable time

...
```

If you want to save the summary in a file just redirect the output

```{code}
$ python parse_checker.py test.json > checks_summary.txt
```

