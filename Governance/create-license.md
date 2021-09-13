# Open Access License

## Why a license?
If you are sharing your data or code freely, you might be wondering why you should be using a license, but making your data freely available to others doesn't mean that you shouldn't establish in which way it can be used. This is where open access licenses come in handy and this is why you can have different flavours of the same open-access license.

Licenses are really useful for both the "data" creator and the user, it helps a potential user to work out quickly if the data is suitable for their intended use and helps them citing and using the data in the way the creator intended.

## Commonly used licenses
Here we summarise the licenses we commonly use. For a much more detailed view of these licenses, ARDC (the Australian Research Data Commons) has a comprehensive guide which covers also copyright.

The important thing to understand about copyright is that it is usually held by or shared with your own institution, even if you are publishing with CLEX. This is because CLEX is not a legal entity and your institution has the Intellectual Property of your work (see below). When you or CLEX applies a license to your data, you are doing so on behalf of your institution. Most institutions have an open-access policy and would be fine with an open-access license unless there are particular circumstances around your data, for example, if it is already covered by an agreement or is of a sensitive nature. If you are in doubt, check with your institution research office if they are fine with the license you want to use.

## Common license rules
Before looking at the different flavours of licenses, we need to understand what they are covering. First of all, these are all open-access licenses so by applying one of them, you are usually giving free access to your data which means that you are not charging for using your data. However, you can regulate how a potential user can access and use your data. Usually, a license will cover some or all of the following points:

* Attribution: a user is required to cite and/or acknowledge your data, this is usually included in any license. You should make sure you are sharing the information on how to cite the data.
* Commercial use and/or research use: you can limit the use of your data to research only or exclude any commercial use of your data.
* Distribution vs private use: if a user can distribute your data/software or can only use it for their own work
* License and copyright notice: a copy of the license and copyright has to be included with the data or software.
* Modification: a user can modify, augment or transform your data to create a new dataset or software
* Same license: the dataset or software resulting from modification of yours has to be distributed under the same license, so they cannot restrict the use of their derived product.
* No-Derivatives: if a user modifies, augments or transforms the data in any way they cannot redistribute it. This can be changed of course if they get in contact with the creator and the creator allows an exception. In fact, this clause is often added only so the creator can be kept informed on how the data is used rather than a strict restriction on derivatives.

The following two points apply only to software:

* Disclose source: source code must be made available when derived product is distributed
* State changes: any changes made must be documented
Finally licenses usually contain a disclaimer to cover warranty and liability, i.e. that the data or software is provided "as is" and that the copyright owner cannot be considered responsible for any damages derived by using the product.

```{admonition} CC-BY 4.0
As you can see there are a lot of different flavours possible. Usually, any license will cover "attribution" which is the most common reason to apply a license: to get your work recognised! If you are unsure which license to use, we advise using the International CC-BY 4.0 license.
```
 
## Dataset license
While we consider both datasets and code as a form of data, from a licensing point of view they are treated differently. For datasets we suggest the Creative Commons licenses (CC). As well as the international version, there is also an Australian Creative Commons. These licenses are simple to use, they offer 6 different flavours, which cover most use cases and an online tool to help you choose between them. They have a human-readable version as well as the legal text and finally, the International version was created to cover your data independently of the potential user's country of origin.

Creative Commons use abbreviation for each of the options:

* BY - for attribution which is always present, the right to distribute is also implicit in any CC license
* NC - for not commercial
* SA - for share alike
* ND - for not derivatives
Check this 5 minutes video to learn more on the available combinations:

[CC kiwi video](https://creativecommons.org/about/videos/creative-commons-kiwi/)


```{admonition} Non-commercial license
In the last few years there is a push to avoid using the Not Commercial clause as this can have unexpected ramifications. For example, if you use some data or an image for a presentation at a conference that people have to pay to attend, this could be considered Commercial use.
```

## Software licenses
For software, you can refer to the Open Source initiative and the Software Sustainability Institute, SSI. They both offer a good introduction, SSI also lists several other websites covering available licenses in a human-readable way and useful comparison tools. Among these:

* [github choose a license tool](https://choosealicense.com/licenses/)

* [TLDR Legal license list](https://tldrlegal.com/licenses/browse)

They both summarise licenses by their "rules".

We usually apply the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0) to the code we produce. Creative Commons are not suitable for licensing software, as stated on the Creative Commons website:

> ... Unlike software-specific licenses, CC licenses do not contain specific terms about the distribution of source code, which is often important to ensuring the free reuse and modifiability of software. Many software licenses also address patent rights, which are important to software but may not be applicable to other copyrightable works. Additionally, our licenses are currently not compatible with the major software licenses, so it would be difficult to integrate CC-licensed work with other free software. Existing software licenses were designed specifically for use with software and offer a similar set of rights to the Creative Commons licenses.

Most of the differences are due to the collaborative nature of most open access code.

Apache 2.0 applies the following

| Permissions | Conditions | Limitations |
| :---------- | ---------- | ----------: |
| Commercial use | | Liability |
| Distribution |   License and copyright notice | Trademark use |
| Modification | State changes | Warranty |
| Patent use | State changes | Warranty |
| Private use | | |

Summarised this means that commercial and private use, distribution and modification are all allowed. A user can also use parts of the code covered by a patent, should there be any, without paying royalties. A user has to attach the original license and copyright notices to any derived product they want to distribute, as well as stating any changes made. Finally, the software creator cannot be held liable for damages and they share the product "as is" with no warranty and the license does not grant trademark rights.

A good insight is again given by [this article](https://opensource.com/article/18/2/how-make-sense-apache-2-patent-license) from the [opensource.com](https://opensource.com/) website.

 
## How to apply a license
Once you have decided which license to apply it is usually fairly easy to apply it to your dataset or code.

If publishing a dataset set you can create a license.txt file which contains the chosen license legal text.

At the top of the file specify the dataset title ( referred to as "licensed material") and the owner of the work you are licensing (referred to as "licensor"). Please note that in the example below CLEX is acting as licensor on behalf of the author and/or their institution.

You can see the license online at

 http://creativecommons.org/licenses/by/4.0/legalcode

> Licensor - ARC Centre of Excellence for Climate Extremes (CLEX) - Level 4, Mathews Building, University of New South Wales, Sydney, NSW, Australia, 2052, Phone: +61 2 9385 9393, e-mail coecss@unsw.edu.au
> Author: "author name" <"author-email">
> Licensed Material - <dataset title> (version 1.0)
> Creative Commons Attribution 4.0 International Public License
> By exercising the Licensed Rights (defined below), You accept and agree to be bound by the terms and conditions of this Creative Commons ....

The license.txt file then will be available both in the dataset local directory and on the NCI dataset catalogue together with the files. Also, we will use the appropriate license link to the Creative Commons website in the files global attributes and in the metadata records we produce.

When publishing or even simply sharing our software, the license is both available in the code repository as a license.txt file and included in the actual files.

```python
 #!/usr/bin/env python
 # Copyright 2019 ARC Centre of Excellence for Climate Extremes
 # author: "author name" <"author-email">
 # 
 # Licensed under the Apache License, Version 2.0 (the "License");
 # you may not use this file except in compliance with the License.
 # You may obtain a copy of the License at
 # 
 #     http://www.apache.org/licenses/LICENSE-2.0
 # 
 # Unless required by applicable law or agreed to in writing, software
 # distributed under the License is distributed on an "AS IS" BASIS,
 # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 # See the License for the specific language governing permissions and
 # limitations under the License.
```

It is important that whichever license you choose the owner, author and title of the work are clear, including the source in case of a derived work. This is the information that anyone who wants to use your work should be using to generate a correct attribution. Even better, you should be providing the preferred citation text yourself.

(this section definitely needs to be updated with more generic content!!!!)
More on intellectual property and copyrights by institution
ANU

Melbourne Uni (need to login to view)

Monash

UNSW

UTAS 

## Q&A
* Does a license last forever?
Technically a license is valid until you hold the copyright, which usually in Australia expires 70 years after creation. You can revoke a license and apply a different one anytime 
* If I move from one license to a different one, would the new one apply in retrospect?
No, a license is an agreement you enter in with someone else at the moment in which they obtain your data/code, so for them the old license will still apply. The new license will apply to anyone who download your data/code from when the license enters in use. If you update your data or code and a "old" user downloads the updates though the new license will apply for them from that moment on.
* What are my options if someone breach the license?
The license is enforceable in court, clearly that's an extreme step, usually people breach the license "accidentally" you should first make contact with them and point out they're breaching the licensing terms and what should they do to amend it. If the breach is of a serious nature contacting the research office of your institution and seek legal advice on the steps to be taken is probably the best course of action.
* How can my license be valid if CLEX or myself act as licensor when the copyright belongs to my institution?
 If you are the creator of the data/code then you can apply a license on behalf of your institution, they won't mind as long as the license you are using is in line with their recommendations. Most of Australian universities and the ARC, which funds most projects, require open access for any research product (unless there is a valid reason not to).

* [Creative Commons FAQ](https://creativecommons.org/faq/)

* [Apache 2.0 FAQ](http://www.apache.org/foundation/license-faq.html)

 
