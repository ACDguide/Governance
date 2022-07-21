# Provenance

Provenance, also referred to as lineage, is the documentation of a dataset origin. It includes how the data was collected or generated, which methodologies, instruments and/or software were used for its creation. You could think of it as the data workflow from the start of a project to the point a dataset is published and you have the project final product.

Provenance can be complex, as usually data gets through a lot of steps and re-iterations. Given the nature of research itself, the objectives and methods of your analysis might change various times, you might keep some of the steps and modify others. Which is why having a good provenance is so important for the reproducibility of your research. There are tools available to help recording some of the steps automatically, but ultimately none of them will produce a good provenance record without regular manual intervention. It is not enough to track the changes you also need to know why they happened.  

**Important things to keep track of are:**

* what data you used as input, if any, it helps if the dataset has been published and has a DOI you can refer to, or it is at least well documented and properly versioned. While there are situations where you do not have choice, when you do you should always prefer a well-documented dataset to one which is poorly documented.
* use a version control system for your analysis code, we recommend `git`. Git and GitHub come with lots of tools and options, make the most of them: readme files, releases, issues, project plans and commit messages, they all help you not only tracking the changes but why they happened.
* if you are using someone else code, as for input data, make sure is properly documented and versioned.
* use good coding practices and metadata conventions for your dataset. Metadata and use of standards make easier sharing data and code, in fact might be required. It will also help you in the future if you need to get back to them after a long break.
* review your provenance often, before you can forget, you could make it a habit at the end of a working day to make sure your previous notes, metadata etc are all still relevant. It will only take a few minutes.

In conclusion provenance is a progressive account of your research, part of the provenance will be directly attached to the data or the code you used, but it is good to have one document that collect all the other sources. A data management plan is a good template for such a document, if you create one at the start of your project and update it regularly you will have your work done when you want to publish the data, when you need to describe your research in a paper, or even before leaving an institution at the end of your PhD or postdoc.

The ARDC also has a lot of [online resources](https://ardc.edu.au/resources/working-with-data/data-provenance/) covering data provenance.
