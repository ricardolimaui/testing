## What is MkDocs?

>MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.
>(Source: [MkDocs](http://www.mkdocs.org/), 2016-03-06)



### Installation

* You need Python (2.7.2) and the Python Package Index (1.5.2) to install and build the documentation. Please make sure that your operating-system provides it, otherwise please install Python before continuing:

```
python --version
pip --version
```

* This documentation is written in Markdown-Syntax. If you are not familiar with Markdown, you can find some nice **Cheat cheets** here:
	* [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
	* [https://daringfireball.net/projects/markdown/](https://daringfireball.net/projects/markdown/)

* Install MkDocs with the following command:

```
pip install mkdocs
```

### Run MkDocs

* If you want to add new content to this documentation, you can use a local repository on your system or edit the pages directly on GitHub.
* First clone this repository to your local-repository

```
git clone https://github.com/geo-c/Dev-Corner.git
```
* MkDocs comes with a build-in-server, which means that all `.md`-files inside the `/docs`-folder will be generated into `.html`-files on-the-fly.
* This is very useful to see your edited files live in your browser
* To start the build-in-server enter the `Dev-Corner/`-folder of your local repository and run the following command:

```
mkdocs serve
```

* Open a new tab in your browser and go to [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

### Contribution

* If you want to add new pages to this documentation, create a new `.md`-Files in folder: `docs/`
**Hint**: If you want to add sections, create a new folder, like this: `docs/NewSection` and create your new `.md`-files in this folder

* Before building, don't forget to add your new page(s) and sections in the `mkdocs.yml`-file. Please find an example at the end of this page: `NewSection` and `newSinglePage.md`

```
- Home: index.md
- Installations:
    - Nodejs: installations/nodejs.md
    - Bower: installations/bower.md
- Data:
    - Collection: data/collection.md
    - Storage: data/storage.md
    - Retrieval: data/retrieval.md
    - Analysis: data/analysis.md
    - Visualization: data/visualization.md
- About:
    - Licenses: about/licenses.md
    - Repositories: about/repositories.md
    - Contributers: about/contributers.md
- NewSection:
    - newPage: newSection/newPage.md
- newSinglePage.md: newSinglePage.md
```

* If you are not familiar with Markdown, please find some **Cheat Cheets** above.
* It is also possible to use HTML-tags inside the Markdown-file, for example a embedded video from Youtube:

```
## Video from Youtube

<iframe width="560" height="315" src="https://www.youtube.com/embed/LRLQE2N0DKc" frameborder="0" allowfullscreen></iframe>
```

* If you have finish your work, please make sure, that there are no errors in the logs of the build-in-server.
* Please commit then your edited files to GitHub.
* Our Main-Server has a cron-job, which will add your files automatically everyday at midnight and convert them into HTML-files.

### Build-process

* As already mentioned, our Main-Server has a cron-job, which will clone the repository automatically everyday at midnight and render the documentation from Markdown to HTML.
* It is also possible to build the HTML-files from your local repository. Before you build it, change the destination inside the `mkdocs.yml`-File:

**Old:**
```
# Local
#site_dir: site
# Server
site_dir: /var/www/html/dev-corner
```

**New:**
```
# Local
site_dir: site
# Server
#site_dir: /var/www/html/dev-corner
```
* **Attention**: Please undo this before you commit your `mkdocs.yml`-file to GitHub!!
* Build documentation with the following command:

```
mkdocs build
```

* **Attention**: If some problems occur during the build-process, you can also try to re-build the documentation with the following command:

```
mkdocs build --clean
```

* The clean-build is useful, if you removed some pages inside the YAML-File, so that the old pages
* All Markdown-Files are now converted to HTML-files into the `site/`-folder. To see your changes your `site/`-folder should be in a Webserver, like an Apache or a Nodejs-Webserver. Otherwise not all functions are working, e.g. the search-function.
* Because MkDocs comes already with an build-in-server, it is highly recommended to use the command `mkdocs serve` and `mkdocs build` only on your published server.
* For more information about MkDocs, please have a look at [http://www.mkdocs.org/](http://www.mkdocs.org/).
