# Climate data guidelines  

## Usage

### Building the book

If you'd like to develop on and build the Climate Data Guidelines book, you should:

- Clone this repository and run
- Run `pip install -r requirements.txt` (it is recommended you do this within a virtual environment)
- (Recommended) Remove the existing `Governance/_build/` directory
   You can do this with
   `jupyter-book clean Governance/`
   `jupyter-book clean Governance/ -all` will also remove the cache
- Run `jupyter-book build Governance/`

A fully-rendered HTML version of the book will be built in `Governance/_build/html/`.

### Hosting the book

The html version of the book is hosted on the `gh-pages` branch of this repo. A GitHub actions workflow has been created that automatically builds and pushes the book to this branch on a push or pull request to main.

If you wish to disable this automation, you may remove the GitHub actions workflow and build the book manually by:

- Navigating to your local build; and running,
- `ghp-import -n -p -f Governance/_build/html`

This will automatically push your build to the `gh-pages` branch. More information on this hosting process can be found [here](https://jupyterbook.org/publish/gh-pages.html#manually-host-your-book-with-github-pages).

NB this should be now automated using github action defined in .github/workflows/deploy.yml
Any commit to the main branch should trigger this action.

## Structure
Currently the book is comprised of 7 parts

1) Guidelines to create a dataset
2) Guidelines to publish a dataset
3) Guidelines to update a dataset (new versions and errata)
4) Guidelines to retire a dataset
5) A section covering data management related concepts: conventions, controlled vocabularies, DMPs etc
6) A section covering technical aspects of data management: compression, chunking, interaction between metadata attributes and software, directory structure, filenames etc.
7) An appendix section for extra materials 

Only the top level of Parts 5 and 6 will be shown in the main table of contents on the book sidebar. So a table of contents is available in the first page of the book to function as an index.
The Guidelines (parts 1-4) will have refernce to the concepts and technical information where appropriate. 

## Contributors

We welcome and recognize all contributions. You can see a list of current contributors in the [contributors tab](https://github.com/ACDguide/Governance/graphs/contributors).

## Credits

This project is created using the excellent open source [Jupyter Book project](https://jupyterbook.org/) and the [executablebooks/cookiecutter-jupyter-book template](https://github.com/executablebooks/cookiecutter-jupyter-book).
