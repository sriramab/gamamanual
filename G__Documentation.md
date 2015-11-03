
# Documentation

The GAMA documentation comes in 2 formats: a set of wiki files availaible from the wiki section of the GitHub website and a PDF file. The PDF file is produced from the wiki files.

In the wiki files, some are hand-written by the GAMA community and some other are generated automatically from the Java code and the associated java annotations.

The section summarizes:
* how to generate this wiki files,
* how to generate the PDF documentation,
* how to generate the unit tests from the java annotations, 
* how to add documentation in the java code.

## Requirements

To generate automatically the documentation, the GAMA Git version is required. See [Install Git version](G__InstallingGitVersion) for more details. 

Among all the GAMA plugins, the following ones are related to documentation generation:
* `msi.gama.processor`: the java preprocessor is called during java compilation of the various plugins and extract information from the java code and the java annotations. For each plugin it produces the `docGAMA.xml` file in the `gaml` directory.
* `msi.gama.documentation`: it contains all the java classes needed to gather all the `docGAMA.xml` files and generate wiki, pdf or unit test files.

In addition, the folder containing the wiki files is required. In the GitHub architecture, the wiki documentation is stored in a separate Git repository `https://github.com/gama-platform/gama.wiki.git`. A local clone of this repository should thus be created:
1. Open the Git perspective:
  * Windows > Open Perspective > Other...
  * Choose `Git`
2. Click on "Clone a Git repository"
  * In **Source Git repository** window: 
    * Fill in the URI label with: `https://github.com/gama-platform/gama.wiki.git`
    * Other fields will be automatically filled in.
  * In **Branch Selection** windows, 
    * check the master branch 
    * Next
  * In **Local Destination** windows,
    * Choose the directory in which the gama Git repository has been cloned
    * Everything else should be unchecked 
    * Finish
3. In the **Git perspective** and the **Git Repositories** view, Right-Click on "Working Directory" inside the `gama.wiki` repository, and choose "Import projects"
  * In the **Select a wizard to use for importing projects** window:
    * "Import existing projects" should be checked
    * "Working Directory" should be selected
  * In **Import Projects** window:
    * **Uncheck « Search for nested project »**
    * Check the project `gama.wiki`
    * Finish
2. Go back to the Java perspective: a `gama.wiki` plugin should have been added.

In order to generate the PDF file from the wiki files, we use an external application named [Pandoc](http://pandoc.org/).
Follow the [Pandoc installation instructions to install it](http://pandoc.org/installing.html). Note that Latex should be installed in order to be able to generate PDF files.


### Configuration

The location where the files are generated (and other constants used by the generator) are defined in the file `msi.gama.documentation/src/msi/gama/doc/util/Constants.java`.

The use of Pandoc (path to the application and so on) is defined in the file `msi.gama.documentation/src/msi/gama/doc/util/ConvertToPDF.java`. *This should be changed in the future...*


### Generated files location
The generated files are (by default) generated in various locations depending on their type:
* wiki files: they are generated in the plugin `gama.wiki`.
* pdf file: they are generated in the plugin `msi.gama.documentation`, in the folder `files/gen/pdf`.
* unit test files: they are generated in the plugin `msi.gama.models`, in the folder `models/Tests`.



## Workflow to generate wiki files

The typical workflow to generate the wiki files is as follow:
* Clean and Build all the GAMA projects,
* Run the `MainGenerateWiki.java` file in the `msi.gama.documentation`,
* The wiki files are generated in the `gama.wiki` plugin.


## Workflow to generate PDF files

The typical workflow to generate the wiki files is as follow:
* Clean and Build all the GAMA projects,
* Run the `MainGeneratePDF.java` file in the `msi.gama.documentation`,
* The wiki files are generated in the `msi.gama.documentation` plugin.


## Workflow to generate unit tests

The typical workflow to generate the wiki files is as follow:
* Clean and Build all the GAMA projects,
* Run the `MainGenerateUnitTest.java` file in the `msi.gama.documentation`,
* The wiki files are generated in the `msi.gama.models` plugin.


## Main internal steps

* Clean and Build all the GAMA projects will create a `docGAMA.xml` file in the `gaml` directory of each plugin,
* The `MainGenerateXXX.java` files then perform the following preparatory tasks:
  * they *prepare the gen folder* by deleting the existing folders and create all the folders that may contain intermediary generated folders
  * they merge all the `docGAMA.xml` files in a `docGAMAglobal.xml` file, created in the `files/gen/java2xml` folder. **Only the plugins that are referred in the product files are merged.**
  
After these common main first steps, each generator (wiki, pdf or unit test) performs specific tasks.
  
### Generate wiki files

* The `docGamaglobal.xml` is parsed in order to generate 1 wiki file per kind of keyword: 
  * operators,
  * statements,
  * skills,
  * architectures,
  * built-in species,
  * constants and units.
  * in addition an index wiki file containing all the GAML keywords is generated.
* One wiki file is generated for each *extension* plugin, i.e. plugin existing in the Eclipse workspace but not refered in the product.

### Generate pdf files

The pdf generator uses the table of content (toc) file located in the `files/input/toc` folder (`msi.gama.documetation` plugin) to organize the wiki files in a pdf file.

* `MainGeneratePDF.java` file parsers the toc file and create the associated PDF file using the wiki files associated to each element of the toc. The generation is tuned using files located in the `files/input/pandocPDF` folder.

### Generate unit test files

* `MainGenerateUnitTest.java` creates GAMA model files for each kind of keyword from the `docGAMAglobal.xml` file.

## How to document
