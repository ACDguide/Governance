(ACDD-conventions)=
# Attribute Convention for Data Discovery
The [Attribute Convention for Data Discovery](https://wiki.esipfed.org/Attribute_Convention_for_Data_Discovery_1-3) covers mostly global attributes which are used to correctly describe shared and published data and to increase its discoverability in data portals. CF conventions recommends only 6 global attributes to define the file content. 
ACDD extends these to include all the information related to the publication of a dataset, adding attributes like: doi, keywords, creator, publisher, etc. The ACDD divides the attributes in three groups: 
* highly recommend - which can be define for any dataset (as 'title') 
* recommend - including attributes that should be define if existing (as
'id' for the DOI) 
* suggested - to further clarify the content but not critical 

When publishing several files as part of the same dataset these attributes should all share the same values, as attributes like "title" should define the "title" of the dataset not of the file itself.NCI requires both CF and ACDD conventions to be applied, they will run a CF/ACDD checker against your files. The CF checker linked above aims to reproduce their process, and can also be used to check against the ACDD conventions. 

```{warning}
Conventions are useful only if the file creator provide the correct values. When you generate a new file from an existing one, the new file will inherit its attributes. It is up to you to make sure they are still valid. If you want to preserve some of the
information from the original file, you can change the attribute name by using a suffix as "source_" or "original_" , so as to clarify they apply to the source file not to the current version.
```
