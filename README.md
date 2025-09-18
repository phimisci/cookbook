# Cookbook
These recipes can be used as [default base configurations](https://pandoc.org/MANUAL.html#defaults-files) for pandoc to process files in the various steps of the production cycle at Philosophy and the Mind Sciences.

The recipes, stored as `.yaml` files in this folder, can be passed to `pandoc --defaults`, e.g.:

```
pandoc --defaults <recipe.yaml> input.md --bibliography input.bib --output <output.file>
```

The file name of each recipe explains its purpose. They are described in more detail below.

> *Note*: The file extension `.yaml` can be omitted in pandoc calls. That is, `pandoc --defaults recipe.yaml` and `pandoc --defaults recipe` are synonymous.

## Contents
  * [Requirements](#requirements)
  * [Installation](#installation)
  * [Import recipes](#import-recipes)
  * [Export recipes](#export-recipes)

## Requirements
- A pandoc installation with version 3.1 or later
- A TeX Live version from 2022 or later
- A terminal app

## Installation
The defaults can be used by downloading/cloning this folder. 

The defaults can be made available system-wide by moving the entire folder, including all templates and filters, to a subfolder in pandoc's user directory. This directory can be found as `User data directory` in the output of `pandoc -v`. 

- On Unix systems your output might look like this:
   ```
   $ pandoc -v
   pandoc 3.1.11.1
   Features: -server +lua
   Scripting engine: Lua 5.4
   User data directory: /home/plato/.local/share/pandoc
   Copyright (C) 2006-2023 John MacFarlane. ...
   ```

- On Windows, the pandoc user directory can usually be found by locating to `%APPDATA%\pandoc` in Windows Explorer.

> *Note*: `pandoc -v` outputs the `user data directory`, but all defaults must be placed in a `defaults` subfolder of that directory. You might have to create this directory. In the Unix example above, it would lie in `/home/plato/.local/share/pandoc/defaults`.

> *Note*: The YAML files containing the defaults must be placed in the root `defaults` folder mentioned above. The `defaults` folder may contain subdirectories (such as for filters or templates), but the YAML recipes must lie in its root.

Once installed there, the defaults can be used from any directory. This is particularly useful if you keep separate subfolders for publication projects.

## Import recipes
### Import from a word processor
Import a odt/doc/docx file to Markdown:
```
pandoc --defaults import-word input.doc --output file.md
```

### Import from Microsoft Word DOCX with Zotero
Import a Microsoft Word (docx only) in which the references have been input using Zotero.
To obtain a .bib database containing the Zotero references, see `export-bibliography-zotero.yaml`.
```
pandoc --defaults import-word-zotero input.docx --output output.md
pandoc --defaults export-bibliography-zotero --output database.bib
```

### Import from a word processor with auto-detection of hand-written citations
Import a Word (odt/doc/docx) file with hand-written citations. The hand-written citations will be searched for in an associated database. This database has to be given via the `--bibliography` argument, e.g.
```
pandoc --defaults import-word-autobib input.md --bibliography database.bib --output file.md
```

After running this file, you might want to check for additional citations that could not be found by the filter. The recipe `export-citation-candidates.yaml` can be used for this:

```
pandoc --defaults export-citation-candidates input.md
```
This second command will print the entire document to your terminal without modifying any exported Markdown files. It will leave a file `citation_candidates.txt` in your working directory. This file contains the citation candidates that you would have to check for manually.

## Export recipes
