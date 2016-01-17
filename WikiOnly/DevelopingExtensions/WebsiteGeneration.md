# How to write the Website Content

_The corresponding architecture presented here is not finished yet, and is hosted currently in the branch **branch_doc_1.7**_

In this page, we will explain all about the convention we use to write and generate the website content and the wiki content.
Since the release of GAMA 1.7, with the new GAMA website, we have two contents:
* The _wiki_ content is hosted in github, witch directly interpret the markdown format of the files to display them in a proper way. This wiki, since it is a wiki, can be edited by any user. It is then, in constant changes.
* The _website_ content is the content of the real GAMA website. It is a verified and fixed version of the documentation (usually a re-generation of the website content is done when there is a new release of the software)

## Index

* [Requirements](#requirements)
* [gama.wiki tree structure](#gamawiki-tree-structure)
* [Good practices when writing markdown files](#good-practices-when-writing-markdown-files)
  * [Title](#title)
  * [Hypertext Links](#hypertext-links)
  * [Images Links](#images-links)
  * [Insert Metadatas](#insert-metadatas)
* [Website Generation Workflow](#website-generation-workflow)
  * [Website Database](#website-database)
  * [Loading the Database](#loading-the-database)

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
* resources: contains all the additional resources needed (images, pdf…)

For the rest of this document, the highest level of tree structure ("Tutorials"/"References"/"Community"/"WikiOnly") will be named as **tabs**. The level just under will be named as **sections**, and the level under will be named as **sub-section**.
All this content is written using the markdown format.
All the images resources are included in the _resources/images_ folder. They are actually under different sub-folders. From the markdown page, you can call the resource with the relative path `resource/images/sub_folder/image_name.png`.
If a _section_/_sub-section_ contains one of several sub-division, then those sub-divisions will be stored in a folder with the name of the corresponding _section_/_sub-section_, and this _section_/_sub-section_ folder will be associated with a markdown file with the same name (indeed, a _section_/_sub-section_ has its own page).
If a _section_/_sub-section_ has no sub-division, then this _section_/_sub-section_ is simply defined with a markdown file containing the content wanted.

![resources/images/developpingExtension/tree_structure.png](resources/images/developpingExtension/tree_structure.png) 

Notice that there is some content which is present only in the wiki (the "WikiOnly" content), some content present only in the website (the model library, most of the community content…). In fact, the wiki tree structure is determined by the file __Sidebar_, while the website tree structure is determined by the file _WebsiteTreeStructure_.

## Good practices when writing markdown files

### Title

Each markdown files **has to** start with a title in the markdown format (like `# title`). This is this title which will be displayed in the tree structure of the website.

### Hypertext Links

Even if the repository how have a more complexe tree structure, you don't have to (and you must not !) speficy the relative or absolute path to the target page, just naming the page will work : `[text_displayed](the_name_of_the_md_file)`

### Images Links

As already said in the [previous paragraph](#gamawiki-tree-structure), images have to be in an "resources/images/folder_name" folder next to your md file, so that you can write the relative path more easily.

### Insert Metadatas

Metadatas in content files are written as comments, with the following syntax:

```
[//]: # (name_of_the_medatada|value_of_the_metadata)
```

Medatadas are not displayed in the wiki and the website content. For the website generation, metadatas are used in order to build the database, most of all to manage the search engine, and the learning graph.

Here is the list of metadata we use in the content files:

* **keyword** : will write an invisible anchor in this exact place in the website. When the user will do a research about this word, he can access directly to this anchor.

* **startConcept**/**endConcept** : used to delimit a concept. The value of those two metadatas is the name of the concept. All the concepts are listed in the file "DependencyGraph", in the content folder in your wiki repository.

#### keyword

The value of the keyword has to have this structure : keyword_category_keyword_name (indeed, several keywords can have the same name ! The type of the keyword has to be specified).
Here is the list of the several keyword categories : concept, operator, statement, architecture, type, constant and skill.
Example of metadata : `[//]: # (keyword|concept_3D)`, or `[//]: # (keyword|operator_int)`.

#### startConcept/endConcept

The value of the keyword have to be one of the values defined in the file learningConcept.xml.

Notice that a _concept_ in the meaning of keyword is not the same as a _concept_ (or _learning concept_) in the learning graph ! 
Please read the part concerning the database to learn more about it.

## Website generation workflow

_This part is not yet implemented, it is under construction._

![resources/images/developpingExtension/website_generation_workflow.png](resources/images/developpingExtension/website_generation_workflow.png)

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


### Website database

![resources/images/developpingExtension/global_database.png](resources/images/developpingExtension/global_database.png)

#### Keyword

A **keyword** is a keyword that can be used for search, either manually (the user enters the wanted keyword in the searchbar of the website) or automatically (through the search tab in the navigation panel)
A keyword in attached with a category (among the following names : concept, type, operator, statement, architecture, constant, action, attribute, skill, facet).
--> A keyword that is a _concept_ can be linked with other keywords (ex : the keyword "BDI" will be linked with the keywords "eval_when", "get_priority"...)
--> A keyword that is a _facet_ is linked to a _statement_ keyword (ex : the keyword "torus" will be linked with the keyword "global").
--> A keyword that is an _action_ or an _attribute_ is linked either to a _skill_ keyword (if it is actually an action or an attribute of a skill), an _architecture_ keyword (if it is an action or a behavior of an architecture) or to a _statement_ keyword (if it is a built-in action or attribute).
--> A keyword that is a _statement_ can be linked to an _architecture_ keyword.

A keyword is composed of:
* **id** (unique id)
* **name** (the word which is searched by the user)
* **idCatagory** (id of the category)

A cagegory is composed of:
* **id** (unique id)
* **name** (the name of the category)

![resources/images/developpingExtension/keyword_table.png](resources/images/developpingExtension/keyword_table.png)

#### Alias

An other database is used to join an **alias** to an existing keyword. Ex : the word "alias" will be changed as "die".

An alias is composed of:
* **id** (unique id)
* **name** (name of the alias. ex : "kill")
* **attachedKeywordName** (name of the keyword attached. ex : "die")

Note that an alias does not know the id of the keyword, but only the name of the attached keyword(s). Indeed, the alias "integer" will give the keyword name "int", but several keywords correspond to the keyword name "int" (it can be the type "int", or the cast operator "int")

![resources/images/developpingExtension/alias_table.png](resources/images/developpingExtension/alias_table.png)

#### Webpage

A **webpage** can be either a page of the model library, a page of the gaml reference, or an other page of the documentation.

A webpage is composed of:
* **id** (unique id)
* **name** (name of the webpage)
* **webpageCategory** (the name of the category of the webpage, a value among _modelPage_, _docPage_, gamlRefPage_).

The tables **webpage** and **keyword** are linked through an association table. This association table contains also an anchor (an anchor has an unique value) to the wanted paged.

![resources/images/developpingExtension/webpage_table.png](resources/images/developpingExtension/webpage_table.png)

Note that only the keywords which have the category _concept_, _type_, _operator_, _skill_ and _constant_ can be attached to a webpage. 
The keywords which have the category _action_, _attribute_ and _facet_ forward to the attached keyword.
The keywords which have the category _statement_ are attached to a webpage only if they are not attached to another keyword. If they are attached to another keyword (an _architecture_ keyword), then the _statement_ keyword forward to the attached keyword.

#### LearningConcept

**LearningConcept** is used to build the learning graph (notice that a "learning concept" and a "keyword concept" is not the same thing !)

A LearningConcept is composed with:

* **id** (unique id)
* **name** (name of the learning concept)

A LearningConcept is linked to a webpage through an association table. This table is composed also with two anchors that are used to delimit the position of the learning concept in a page (the beginning position and the ending position).

A LearningConcept can be associated to other LearningConcepts through an association table, used to spefify the "prerequisite concepts".

![resources/images/developpingExtension/learningConcept_table.png](resources/images/developpingExtension/learningConcept_table.png)

### Loading the Database

The database is loaded from a gathering of independent files. Some of those files are handmade written, other are generated automatically.

#### Role of the documentation generation script in the construction of the database

As explained in the explication of the [documentation generation pages](Documentation), the documentation generation script is used to generate the gaml references and the model library pages (in the markdown format with metadatas), but also to build two files **category.txt** and **keyword.xml**.

The file **catagory.txt** is a very simple file, listing the different keyword categories. This file will be used to build the **Catagory** table.

Format of the file:
```
concept, type, statement, architecture, operator, skill, constant, action, attribute, facet
```

The file **keyword.xml** is an xml file that contains all the possible keywords (all except some keywords written manually directly in the documentation pages). The GAML words can be found directly using the code of GAMA. The concept words can be found using the code of GAMA (thanks to the tag "catagory") and also by using the tags in the header of the model files. This xml file will be used to build the **Keyword** and the **AssociationKeywordCatagory** tables.

Format of the file:
```
<keyword id:keywordname_keywordcategory>
  <name>keywordname</name>
  <category>keywordcategory</category>
  <associatedKeywordList>
    <associatedKeyword>keywordId1</associatedKeyword>
    <associatedKeyword>keywordId2</associatedKeyword>
  </associatedKeywordList>
</keyword>
```

Note that:
--> The list associatedKeywordList contains only one element for the _facet_ keywords, one of no element for the _action_ or _attribute_ keywords (none when the action/attribute is a built-in), several or no elements for the _concept_ keywords, and none for the other type of keywords.
--> The id is build with the value of the attribute "name" and with the value of the attribute "category" for every keywords except the _statement_, _facet_, _action_ and _attribute_ keywords, which need also the value of the associatedKeyword linked. Ex : the id of the facet "torus" will be "facet_torus_statement_global".

#### Preparation of the repository before the generation of the database

After the generation of the markdown content in the wiki repository, two other files have to be built manually : the files **alias.txt** and **learningConcept.xml**.

The **alias.txt** file contains all the connexions between alias and keyword name. It will be used to build the **Alias** table.

Format of the file :
```
aliasName1:remplacedWord1
aliasName2:remplacedWord2
kill:die
```

The **learningConcept.xml** file is used to list the learning concepts, and to connect them to their prerequisite concepts. It will be used to build the **LearningConcept** and the **AssociationLearningConcept** tables.

Format of the file :
```
<learningConcept id:learningConceptName>
  <name>learningConceptName</name>
  <prerequisiteList>
    <prerequisite>learningConcept1</prerequisite>
    <prerequisite>learningConcept2…</prerequisite>
  </prerequisiteList>
</learningConcept>
```
Note that the value of the attribute "name" can be used as an unique id.

#### Role of the website content generation script in the construction of the database

After copy-paste the content to the website folder, a script is used to build the database and to generate website content.

The **Category**, **Alias**, **LearningConcept** and **AssociationLearningConcept** tables are loaded easily from the files **category.txt**, **alias.txt**, and **learningConcept.xml**.

The **Keyword** and **AssociationKeywordCategory** tables are loaded from the **keyword.xml** file. Note that those two tables are not entirely loaded yet, because other keywords can be presents in the header of other files.

The markdown files are converted one by one into html format.
--> When a metadata **startConcept**/**endConcept** is found (syntax : [//]: # (beginAnchor|name_of_learning_concept)), the metadata is replaced with an anchor in the page (with an unique id), and the **AssociationWebpageConcept** table is updated.
--> When a metadata **keyword** is found (syntax :  [//]: # (keyword|name_of_keyword_category_name_of_keyword)), the metadata is replaced with an anchor in the page (with an unique id), and the **AssociationWebpageKeyword** table is updated (the **Keyword** and **AssociationKeywordCategory** are updated if the keyword does not exist yet in the table).
