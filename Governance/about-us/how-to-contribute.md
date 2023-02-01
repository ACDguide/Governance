# Guidelines for contributors

Contributions to the Jupyter Book are welcomed and encouraged, and we welcome and recognise all contributions. You can see a list of current contributors in the [contributors](https://github.com/ACDguide/Governance/graphs/contributors) tab.

The Jupyter Book is hosted on Github and can be edited by creating a pull request. 
How to collaborate with pull requests on Github: https://docs.github.com/en/github/collaborating-with-pull-requests. Jupyter Book documentation: https://jupyterbook.org/intro.html.


## Outline of steps to contribute
1. Open an issue with any updates you think are needed. This is helpful to keep track of changes being made to the book.
2. Make the updates/edits (see steps below) as a PR from your local fork to the base repo.
3. Assign someone to review your PR (see steps below). 
4. Merge the PR once it has been approved.

### Steps to make edits/updates to this book
- **Fork the base repository.** You can do this by clicking "Fork" in the upper right corner of the window. This will clone (i.e. copy) the base repo into your own account, so you should now have a repo at [your-gh-username]/Governance that is identical to the base repo.
- **Make the edits or updates in your own fork.** You can now update the content of your forked version of /Governance. Depending on preference, you can create a new branch in your forked repo and make all updates within your new branch, or you can update the main branch directly. Edits can be made in a number of ways:
  - From your forked repo, type the "." key to open a VSCode editor directly in your browser. You can make edits/additions and commit them directly to your forked repo.
  - You can clone the base repo to your local computer (see instructions [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)) and use whatever editor you choose to make edits. If you do this, it is recommended that you add two remote repos by setting "origin" to your forked repo and "upstream" to the base repo (see instructions for adding remote repo [here](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)). 
- **Open a pull request (PR) to the base repo.** GitHub has made this easy for us with an option just above the list of files in our forked repo. You should see a banner that says something like "This branch is 1 commit ahead of ACDguide:main." To the right, there is a drop-down button to "Contribute" and "Create pull request". Click that and it takes you to a page that shows the updates you have made. Then click "Create pull request" and give the PR a title and description if needed. Then click "Submit" and your updates will show up in the "Pull Requests" tab of the base repo! To link your PR with its corresponding issue, type "Resolves #[issue-number]", and this will automatically close the issue that this PR resolves. If your PR does not resolve, but is related to an issue, then you can simply reference the issue by typing "#[issue-number]".

**No edits should be made to the main branch of ACDguide/Governance (the base repository), unless correcting minor typos.**

#### Reviewing/commenting on PRs
- Assign someone to review your PR. This can be done by clicking the gear in the upper right of the PR next to "Assignees". A drop-down menu of all maintainers should appear and you can choose the appropriate person or people.
- Who should you ask to review your PR? It depends on the page you are updating.
  - `Creating climate data`: Chloe (@chloemackallah)
  - `Publishing climate data`: Paola (@paolap)
  - `Updating published data`: Claire (@hot007)
  - `Retiring published data`: Claire? (@hot007)
  - `Computations with large datasets`: see [Guide for Working with Big/Challenging Data Collections](https://github.com/ACDguide/BigData)
  - any other pages, for structural changes, or if you are unsure who to assign: Chloe (@chloemackallah)

- You can also assign multiple reviewers if you think your PR would benefit from other/more reviewers.