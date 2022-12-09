(data-license)=
# Dataset license
Datasets and software are both research products, from a licensing point of view they are treated differently. For datasets we suggest applying one of the [Creative Commons licenses (CC)](https://creativecommons.org/licenses/). 
 These licenses are simple to use, they offer 6 different flavours, which cover most use cases and an [online tool](https://chooser-beta.creativecommons.org) to help choosing between them. They have a human-readable version as well as the legal text and finally, the International version was created to cover your data independently of the potential user's country of origin.

```{note}
As well as the international version, there is also an [Australian Creative Commons](https://creativecommons.org.au/).
```

Creative Commons uses an abbreviation for each of the options:

* **BY** - for attribution which is always present, the right to distribute is also implicit in any CC license
* **NC** - for not commercial
* **SA** - for share alike
* **ND** - for not derivatives
Check the [CC kiwi video](https://creativecommons.org/about/videos/creative-commons-kiwi/) (5 minutes long) to learn more on the available combinations.


```{admonition} Not Commercial option 
:class: warning
In the last few years there is a push to avoid using the Not Commercial clause as this can have unexpected ramifications. For example, if you use some data or an image for a presentation at a conference that people have to pay to attend, this could be considered Commercial use.
```

## How to apply a license
Once decided which license to apply, it is usually easy to apply it to a dataset.

When publishing a dataset add a `license.txt` file which contains the chosen license legal text.

At the top of the file specify the dataset title ( referred to as "licensed material") and the owner of the work you are licensing (referred to as "licensor"). Please note that in the example below CLEX is acting as licensor on behalf of the author and/or their institution.


**Example license header**
> Licensor - ARC Centre of Excellence for Climate Extremes (CLEX) - Level 4, Mathews Building, University of New South Wales, Sydney, NSW, Australia, 2052, Phone: +61 2 9385 9393, e-mail coecss@unsw.edu.au<br>
> Author: "author name" <"author-email"><br>
>  Licensed Material - <dataset title> (version 1.0)<br>
>  Creative Commons Attribution 4.0 International Public License<br>
>  By exercising the Licensed Rights (defined below), You accept and agree to be bound by the terms and conditions of this Creative Commons ....

The `license.txt` file then will be available both in the dataset local directory and on the online data portal together with the files. Also, as netCDF is self-describing the appropriate license link to the Creative Commons website can be added to the files global attributes and/or other metadata records available.

It is important that whichever license is chosen, the owner, author, and title of the work are clear, including the source in case of a derived work. This is the information that anyone who wants to use the data should be using to generate a correct attribution. Ideally, the author should provided the preferred citation.

```{note} CC-BY 4.0
There are a lot of different flavours possible. Usually, most licenses cover "attribution" which is the most common reason to apply a license: to get your work recognised! If unsure about which license to use, we advise using the [International CC-BY 4.0 license](https://creativecommons.org/licenses/by/4.0/legalcode).
```

