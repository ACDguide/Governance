# Software licenses
The [Open Source initiative](https://opensource.org/licenses) and the [Software Sustainability Institute (SSI)](https://software.ac.uk/resources/guides/choosing-open-source-licence?_ga=2.23847290.1503282406.1562136302-1313042888.1562136302) offer a good introduction to software licensing. SSI also lists several other websites covering available licenses in a human-readable way and useful comparison tools. Among these:

* [GitHub Choose a license tool](https://choosealicense.com/licenses/)

* [TLDR Legal license list](https://tldrlegal.com/licenses/browse)

They both summarise licenses by their "rules".

As for the data, the ARDC has also a [guide to software licensing](https://ardc.edu.au/resource/research-software-rights-management-guide/). It is also worth noticing that the ARDC is running several initiative to facilitate software sharing and publishing.

Permissive software license, also known as BSD-like or BSD-style licenses, are free-software licenses which carry only minimal restrictions on how the software can be used. 
Two of the most used permissive licenses are the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0) and the [MIT license](https://choosealicense.com/licenses/mit/).

## Apache 2.0

Apache 2.0 applies the following

| Permissions | Conditions | Limitations |
| :---------- | ---------- | ----------: |
| Commercial use | License and copyright notice | Liability |
| Distribution | State changes | Trademark use |
| Modification | | Warranty |
| Patent use |  | |
| Private use | | |

Summarised this means that commercial and private use, distribution and modification are all allowed. A user can also use parts of the code covered by a patent, should there be any, without paying royalties. A user has to attach the original license and copyright notices to any derived product they want to distribute, as well as stating any changes made. Finally, the software creator cannot be held liable for damages and they share the product "as is" with no warranty and the license does not grant trademark rights.

A good insight is again given by [this article](https://opensource.com/article/18/2/how-make-sense-apache-2-patent-license) from the [opensource.com](https://opensource.com/) website.

## MIT license

| Permissions | Conditions | Limitations |
| :---------- | ---------- | ----------: |
| Commercial use | License and copyright notice | Liability |
| Distribution | | Warranty |
| Modification | | |
| Private use | | |

The MIT license is a short and simple permissive license with conditions only requiring preservation of copyright and license notices. Licensed works, modifications, and larger works may be distributed under different terms and without source code.
 
## How to apply a license

When publishing or even simply sharing our software, the license is both available in the code repository as a license.txt file and included in the actual files.

Example of code with license header:

> \#!/usr/bin/env python <br>
> \# Copyright 2019 ARC Centre of Excellence for Climate Extremes  <br>
> \# author: "author name" <"author-email">  <br>
> \#  <br>
> \# Licensed under the Apache License, Version 2.0 (the "License");  <br>
> \# you may not use this file except in compliance with the License.  <br>
> \# You may obtain a copy of the License at  <br>
> \#  <br>
> \#     http://www.apache.org/licenses/LICENSE-2.0  <br>
> \#  <br>
> \# Unless required by applicable law or agreed to in writing, software  <br>
> \# distributed under the License is distributed on an "AS IS" BASIS,  <br>
> \# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  <br>
> \# See the License for the specific language governing permissions and  <br>
> \# limitations under the License.

It is important that whichever license you choose the owner, author and title of the work are clear, including the source in case of a derived work. This is the information that anyone who wants to use your work should be using to generate a correct attribution. Even better, you should be providing the preferred citation text yourself.

```{warning}
Creative Commons are not suitable for licensing software, as stated on the Creative Commons website:

> ... Unlike software-specific licenses, CC licenses do not contain specific terms about the distribution of source code, which is often important to ensuring the free reuse and modifiability of software. Many software licenses also address patent rights, which are important to software but may not be applicable to other copyrightable works. Additionally, our licenses are currently not compatible with the major software licenses, so it would be difficult to integrate CC-licensed work with other free software. Existing software licenses were designed specifically for use with software and offer a similar set of rights to the Creative Commons licenses.

Most of the differences are due to the collaborative nature of most open access code.
```

