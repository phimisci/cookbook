# Cookbook
These recipes can be used as default base configurations for pandoc to process files in the various steps of the production cycle at Philosophy and the Mind Sciences.

The recipes, stored as `.yaml` files in this folder, can be passed to `pandoc --defaults`, e.g.:

```
pandoc --defaults <recipe.yaml> input.md --bibliography input.bib --output <output.file>
```

The file name of each recipe explains its purpose. They are described in more detail below.

## Contents
  * [Requirements](#requirements)
  * [Import recipes](#import-recipes)
  * [Export recipes](#export-recipes)

## Requirements
- A pandoc installation
- A TeX Live version from 2022 or later
- A terminal app

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
