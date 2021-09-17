# Choosing a directory structure (DRS) and filenames

The names you choose for files and directories and generally the way you organise your data, i.e. your directory structure (DRS) can help navigating the data and provide extra information, avoid confusion and the user ending up accessing the wrong data. As for many other cases the best file organisation will depend on the specific research project and the actual server where the data is stored. Here we are just listing a few guidelines and tips to help you decide.  

## General considerations
 Familiarise yourself with the storage system, make sure you are storing the files in the most appropriate place, get to know if the storage is backed up or not, what is your allocation, and also what rules or best practices apply.
Take into account how yourself or others might want to use the data, this is particularly important when deciding the DRS but also how to divide data across files for big dataset as model output. Doing so at the start of the project will spare you lots of time you might otherwise spend re-processing all your files.
Be consistent, this applies both to the organisation and the naming, consistency is essential for the data to be machine-readable, i.e. data which is easy to access by coding. In fact, use community standards and/or controlled vocabularies wherever possible.
Consider adding a readme file in the main directory (we always do that for data we publish), including an explanation of the DRS and the naming conventions, abbreviation and/or codes you used. If you used standards and controlled vocabularies all you have to do is to include a link to them.    

## DRS

![Example of directory structure](../images/example_drs.png)

The figure above shows an example of an organised working directory for a model output, things to consider:

* try to organise files in directories based on type and how you process them
for the final output think also about how other might use them: are they going to be used for analysis or they could be used as forcing or restart files for a model? 
* think of the way you would access these directories in a code, as an example having the variable directories using exactly the same name as the actual variable
* make sure your code is separate from your data, you want to be able to use something like git to version control it and possibly GitHub to back it up easily
* have at least one readme file with detailed metadata, possibly more if you have a lot of directories/files. You cannot use git for keep manage versions of data but you can use git to version control your readme files.
* review at regular intervals what you are keeping, what needs to be removed and how things are organised
