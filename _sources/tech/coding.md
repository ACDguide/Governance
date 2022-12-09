# Coding best practices

There are code standards and conventions available depending on the language you are using (see references below) and sometimes also conventions adopted for specific collaborative projects. These can be complex and out of scope for smaller projects and/or a simple code. This page lists a few simple tips to make a code readable and safer from bugs.<br>
 In the video linked below, kindly provided by DataTAS, the presenter gives some useful tips which can be applied to any language:

"Reproducible research how to write code that is built to last" 

It is worth watching the video (the actual presentation is about half of the video ~35 minutes) to understand fully how valuable these tips are and also to get a perspective from someone who went from a science background to a commercial software engineering position.

Below is a list of best practices discussed in the video.

**Naming**
* Use descriptive names for variables and functions
* Use consistent naming across the code
* Avoid hard-coding values
* Initialising variables
**Code structure**
* Indents
* Comments
* Use functions to organise your code 
* Don't Repeat Yourself (DRY) code
* One statement per line
* Write explicit code
* Keep your files a reasonable length
* Clear flow: try to have only one exit point in a function
* Test important parts of your code  

## Writing reusable code

Basic

The basics of code reusability involve easily readable code and DRY (don't repeat yourself) principles, so using functions/subroutines/procedures to avoid copying blocks of code and modifying each block. The tips in the introduction can all help with code reusability as well as those listed below.

Ten tips for writing readable code (based on PHP but principles are universal):

https://dzone.com/articles/10-tips-how-to-improve-the-readability-of-your-sof 

A good (python specific) section of a course from Software Carpentry about writing functions:

https://swcarpentry.github.io/python-novice-inflammation/08-func/index.html

For the beginner python programmer it can be difficult to know exactly how to go about reusing code, how to organise it and import it into your notebooks or programs. This is a short, clear article about the python specific details on reusing your code:

https://towardsdatascience.com/creating-reusable-code-for-data-science-projects-740391ec7bad

In a similar vein (and also python specific), how and when to use a main function in python:

https://realpython.com/python-main-function/

Intermediate

Once code style, readability and DRY principles hace been mastered the next step is improving what you're already doing and using the more advanced language features.

This is a really nice and clear (FORTRAN specific) explanation of how to move from a purely procedural approach, explaining progressively more advanced features of FORTRAN functions and subroutines, and finishing with a real-world scientific example program:

https://livebook.manning.com/book/modern-fortran/chapter-3/62

Unfortunately the above link is to a book (Modern Fortran) only part of which is freely viewable. Ideally the book may be available institutionally, but if there is an equivalent freely available link let us know.

 

Advanced

To see the advice above put into practice, you can watch this video. It is a bit long (18min). It is under the Advanced resources because the code it is using is written in Rails. Not many of you will have experience in Rails but the purpose of the video is to talk about the principles and not the specificity of the code. It also involves some more advanced concepts such as classes and modules.

Documentation plays a critical role for code reusability. Any effort to document code is worthwhile and will improve reusability, but it is likely a large effort in code documentation will only be made in advanced code reuse scenarios, like a published module or library. In that scenario this is an excellent introduction primarily about  taking into account the audiences for different aspects of code documentation:

https://documentation.divio.com/introduction/

 

### Style guides
Python: 
* [pep8 Style guide for Python code](https://peps.python.org/pep-0008/)
* [Code style](https://docs.python-guide.org/writing/style/) from The Hitchhiker's Guide to Python
* [How to Write Beautiful Python Code With PEP 8](https://realpython.com/python-pep8/) from realpython.com
* [Python reserved keywords](https://realpython.com/lessons/reserved-keywords/)

Julia:
* [Julia style guide](https://docs.julialang.org/en/v1/manual/style-guide/)
* [Julia reserved keywords](https://docs.julialang.org/en/v1/base/base/#Keywords)

R:
* [R style guide](http://adv-r.had.co.nz/Style.html) from Advanced R by Hadley Wickam
* [R style guide](https://style.tidyverse.org) used in Tidyverse
* [R reserved keywords](https://www.datamentor.io/r-programming/reserved-words/)

