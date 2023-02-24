# Version Control

**Version Control systems** (e.g. git, SVN) are used to track changes to files over time, so that if a mistake is introduced, it is possible to go back to an earlier copy to work out what changed.

Version control is particularly useful with code development, but it can also be used with documents (for example this book!) or pretty much any other file.

You would typically use not just local version control, that is, making a history of our code as you develop it, but pair the use of `git` with a **remote repository** on a server such as GitHub (global cloud), GitLab (e.g. NCI's git hosting instance) or BitBucket (e.g. CSIRO's hosting instance). This means there are at least two copies of your repository so if something catastrophic happens in your local copy, you can always pull a fresh copy from the remote server. It also allows you to pull a copy of the repository to wherever you are working, for example, your work computer, home computer, or a remote machine such as NCI's HPC or cloud.

There are a number of useful concept introductions to version control which are linked to here rather than attempting to paraphrase:
* [Git-SCM's introduction to version control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) - excellent overview of concepts and a useful resource generally
* [GitLab's about version control](https://about.gitlab.com/topics/version-control/) - shorter and less depth
* [Towards Data Science tutorial on getting started with Git](https://towardsdatascience.com/git-and-github-basics-for-data-scientists-b9fd96f8a02a) - hands on examples of setting up a repository

## When to use version control

* **When developing code**, even if it's just for yourself, undoing mistakes and checking differences is much easier with version control. Additionally having a remote backup protects against disaster.
* **When sharing code**, it is easy for a collaborator to pull a copy of your code to their own machine, then if you make changes they can easily pick up your changes, and reciprocally, you may permit your collaborators to also make changes to your code base directly or via "pull request".
* **When collaborating on a large central body of code**, it is best practise to "fork" a copy of the respository, make modifications in your own branch, and then submit a "pull request" for your modifications to be merged into the authoritative version of the code.

## When not to use version control

Some files are not suited to being housed in a repository, either because it is inappropriate, or because they may blow out the size of the repository. 

Files that wouldn't usually be included in a version control system are compiled binaries (they are probably not portable to other machines), large data files (host them elsewhere if needed for tests), and local settings files.

It is okay to have files in your git-managed directory that are not included in the version controlled repository - you can *exclude* files from version control using a `.gitignore` file in git, which is simply a text list of files in the git directory which should not be checked by git for changes or suggested for staging.

## Additional resources

There are many excellent resources to help getting started with version control, as well as style guides and coding best practices.

This [CMS blog post](http://climate-cms.wikis.unsw.edu.au/Coding_best_practices) contains a number of useful tips and links for researchers at various stages of coding practice.