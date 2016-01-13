# How to write the Website Content

_The corresponding architecture presented here is not finished yet, and is hosted currently in the branch **branch_doc_1.7**_

In this page, we will explain all about the convention we use to write and generate the website content and the wiki content.
Since the release of GAMA 1.7, with the new GAMA website, we have two contents:
* The _wiki_ content is hosted in github, witch directly interpret the markdown format of the files to display them in a proper way. This wiki, since it is a wiki, can be edited by any user. It is then, in constant changes.
* The _website_ content is the content of the real GAMA website. It is a verified and fixed version of the documentation (usually a re-generation of the website content is done when there is a new release of the software)

## Index

* [Requirements](#requirements)
* [Gama.wiki tree structure](#gamawiki-tree-structure)
* [Good practices when writing markdown files](#good-practices-when-writing-markdown-files)
  * [Title](#title)
  * [Hypertext Links](#hypertext-links)
  * [Images Links](#images-links)
  * [TODO parts](#todo-parts)
* [CheckURL Script](#checkurl-script)
* [Website Generation Workflow](#website-generation-workflow)

## Requirements

To generate automatically the documentation, the GAMA Git version is required. See [Install Git version](G__InstallingGitVersion) for more details.

Among all the GAMA plugins, only one is related to documentation generation:
* `msi.gama.documentation`: it contains some useful java scripts to help you to write a correct documentation.

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
    * **Uncheck « Search for nested project »**
    * Check the project `gama.wiki`
    * Finish
2. Go back to the Java perspective: a `gama.wiki` plugin should have been added.

## gama.wiki tree structure

The "gama.wiki" plugin contains all the wiki content, and almost all the website content. It contains a folder content which contains the following folders:
* Tutorials
  * LearnGAMLStepByStep: contains the linear documentation to learn about the concepts of GAML
  * Recipes: contains short pieces of documentation answering a specific problematic
  * Tutorials: contains applicative tutorials 
* References
  * ModelLibrary: contains the model library (only present in the website) 
  * PlatformDocumentation: contains the documentation dealing with how to use the platform
  * GAMLReferences: contains GAML references
  * PluginDocumentation: contains the documentation of the additional plugins
* Community
  * Projects: contains a presentation of the projects where GAMA is involved (only present in the website)
  * Training: contains a presentation of the training sessions organized by the GAMA team (only present in the website)
* WikiOnly: contains the content only present in the wiki, and not in the website
  * DevelopingExtensions: contains explanations about how to extend the platform
* ressources: contains all the additional resources needed (images, pdf…)

For the rest of this document, the highest level of tree structure ("Tutorials"/"References"/"Community"/"WikiOnly") will be named as **tabs**. The level just under will be named as **sections**, and the level under will be named as **sub-section**.
All this content is written using the markdown format. 
The folder _images_ is present in every folder. It contains images files that are used from the files in the corresponding folder (so that the file which needs an image will call it with the relative path `ìmages/name_of_the_image.png`).
If a _section_/_sub-section_ contains one of several sub-division, then those sub-divisions will be stored in a folder with the name of the corresponding _section_/_sub-section_, and this _section_/_sub-section_ folder will be associated with a markdown file with the same name (indeed, a _section_/_sub-section_ has its own page).
If a _section_/_sub-section_ has no sub-division, then this _section_/_sub-section_ is simply defined with a markdown file containing the content wanted.

[images/websiteContent/images_by_section.png](images/websiteContent/images_by_section.png) 

Notice that there is some content which is present only in the wiki (the "WikiOnly" content), some content present only in the website (the model library, most of the community content…). In fact, the wiki tree structure is determined by the file __Sidebar_, while the website tree structure is determined by the file _WebsiteTreeStructure_.

## Good practices when writing markdown files

### Title

Each markdown files **has to** start with a title in the markdown format (like `# title`). This is this title which will be displayed in the tree structure of the website.

### Hypertext Links

Hypertext links have to be written with the following syntax: `[text_displayed](your_link_url)`. You can write your hypertext link in other format of course (`<a href=…`), but better uniform the ways of writing things down (and with the first syntax asked, you will be able to run the [_CheckURL_ script](#checkurl-script), which may help you a lot). 

### Images Links

As already said in the [previous paragraph](#gamawiki-tree-structure), images have to be in an "images" folder next to your md file, so that you can write the relative path more easily.

### TODO parts

If, when you are writing the documentation, there is a topic you have not finished, do not hesitate to write a "TODO", or a "Under construction" in the documentation, just as a reminder (Those syntaxes will be find easily thanks to the [_CheckURL_ script](#checkurl-script).

## CheckURL script

The checkURL script is part of the _msi.gama.documentation_ plugin, in the _msi.gama.doc.checkURL_ package. This script is useful to make quick URL changes, and also to tell you some useful informations about the content, in order to avoid mistakes (like dead links for instance).

The checkURL script will first need the content folder, which has to be specified in a file called _localPath.txt_ in the _msi.gama.documentation_ folder. Then, it will scan all the folder contained inside this content folder, and store in a map the path to all the markdown files (the name of the file is the key, the url path is the value). 
Then, the script will browse all the markdown files, searching for the `[text_displayed](your_link_url)` syntax. Once one is find, some verifications and/or modifications are done:
* If the link is a link to an image (which means a relative link), no modifications are done. An error message appears if the image does not exist.
* If the link is an anchor to the actual page, nothing is done (we hope the anchor is correct…)
* If the link is a link to another page,
  * if the link exists in the map, nothing is done.
  * if the link does not exist in the map, and if the file name is isolated from the rest of the path is a key of the map, then we change the old path by the new one (and we print a message)
  * if the link starts with an url to the github gama source, then we try to find if the file exists. An error message appears if the file does not exist.
  * if the link starts with an url to the github wiki content, then we try to find if the file exists. An error message appears if the file does not exist.
  * if the link is an url to the www, nothing is done.
  * if none of those conditions are fulfilled, an error message appears, telling that this link could not be verified.

In the same time, the CheckURL script also check if all the images (more precisely all the files in an "images" folder) have been used. If it is not the case, the unused images are listed as a warning point. We don't want dead resources!
At last, CheckURL searches if some _forbidden syntax_ are present, and present you how many times those syntax are used in the code. Here is the list of forbidden syntax:
* The "TODO" and the "Under construction" message: those syntax in the code indicates that the documentation is not finished. A useful reminder.
* The links with the syntax `<a href=…` or `<img src=…` are not checked with the checkURL script. You have to check those links manually, so try to avoid them as much as possible.

## Metadatas

_This part is still fuzzy. We have to think about an efficient way to use those metadatas_


Metadatas in content files are written as comments, with the following syntax:

```
[//]: # (name_of_the_medatada::value_of_the_metadata)
```

Medatadas are not displayed in the wiki and the website content. For the website generation, metadatas are used in order to build the database, most of all to manage the search engine, and the learning graph.

## Website generation workflow

_This part is not yet implemented, it is under construction._

[images/websiteContent/website_generation_workflow.png](images/websiteContent/website_generation_workflow.png)

### The gama.documentation plugin

This plugin is used to [generate GAML documentation automatically in the markdown format](G__Documentation), and copy paste the content to the wiki folder.
The plugin is also used to generate the model library in the markdown format, with the source code, a quick description, and an image (screenshot). In the same time, the plugin generates a html page (an "abstract") and put it directly in the model folder (in order to be loaded directly from GAMA).

### The gama.wiki repository

This repository contains in on hand the content auto generated by the documentation plugin, and in the other hand a handmade content. All the content is in the markdown format, organized through a [specific tree structure](#gamawiki-tree-structure), sometime containing [metadatas](#metadatas).

### The website repository

This repository contains:
* A copy of the content of the wiki repo (copy/pasted manually to freeze a specific commit of the wiki)
* A Database management system
* A script used to interpret the metadatas from the content, in order to load the database
* Some pages which are not in the wiki repo, and some heavy resources (such as videos)
 
