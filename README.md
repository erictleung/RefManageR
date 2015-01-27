RefManageR
========
RefManageR provides tools for importing and working with
bibliographic references.  It greatly enhances the bibentry class by
providing a class BibEntry which stores BibTeX and BibLaTeX references,
supports UTF-8 encoding, and can be easily searched by any field, by date
ranges, and by various formats for name lists (author by last names,
translator by full names, etc.). Entries can be updated, combined, sorted,
printed in a number of styles, and exported. BibTeX and BibLaTeX .bib files
can be read into R and converted to BibEntry objects.  Interfaces to NCBI's
Entrez, CrossRef, and Zotero are provided for importing references and
references can be created from locally stored PDFs using Poppler.  Includes
functions for citing and generating a bibliography with hyperlinks for
documents prepared with RMarkdown or RHTML.

Please see the [vignette](http://cran.r-project.org/web/packages/RefManageR/vignettes/manual.pdf).

NEWS
=====================================
Changes in Version 0.8.52 (2014-01-26)
--------------------------------------------------------

NEW FEATURES

* `GetPubMedByID`: Now returns some additional fields including 'month' and 'issn' for
articles; will print a warning if PubMed does not return the complete list
of authors; will use the name of a collective if one is available and the individual
authors are missing (h/t Dale Steele)

BUG FIXES

* `ReadBib`: If a name list field in an entry cannot be parsed in the bib file, the
entry will be ignored, but the rest of the file will still be processed and
returned. In the past, this caused an error and no output would be returned.
* 'Book' entries will now be parsed correctly by `GetPubMedByID` (h/t Dale Steele)
* Fix error/warning messages when entry is missing required fields (introduced in
Version 0.8.45)
* Name lists containing a comma in braces will now be parsed correctly,
e.g. "Buchalter, Louis and {Murder, Inc.} and Anastasia, Albert"


Changes in Version 0.8.45 (2014-12-29)
--------------------------------------------------------

BUG FIXES

* `ReadCrossRef` now correctly handles the small number of cases where BibTeX information
cannot be obtained for a particular DOI, which resulted in 'stack imbalance' warnings
and no results being returned (h/t Norman L Guinasso Jr).
* `ReadGS` fixed to account for changes to Google "API" (h/t Norman L Guinasso Jr).
* Improved parsing for BibTeX format names ending with a '}' (h/t Henrik Bengtsson).
* Printing references with `style = "html"` would not always add an opening <cite> tag
when `bib.style = "numeric"` or `bib.style = "alphabetic"` (h/t Henrik Bengtsson).
* `format.BibEntry` would ignore the `.style` argument if called directly by the user.
Note, this function should normally not need to be called directly. (h/t Henrik Bengtsson)

Changes in Version 0.8.40 (2014-10-28)
--------------------------------------------------------

NEW FEATURES

* Improved formatting of citation given to CrossRef for increased chances of finding matches with `GetDOIs`
function (h/t Erich Studerus)
* Additional parsing of 'month' field to accomodate days and ranges of days and months.  Example bib entries
that will be parsed correctly include `month = jun # "/" # jul`, `month = "20~" # jan`,
`month = "20--25~" # dec`, `month =  "10~" # jan # "/" # feb` (request of Stephen Eglen)
* Added argument 'group' to `ReadZotero` for specifying a groupID to query a group library instead of a
user library (h/t Greg Blomquist).

BUG FIXES

* DOI's hyperlinks in Markdown format are now correct (h/t Stephen Eglen)
* `print.BibEntry` with `BibOptions(style = "Biblatex")` fixed (h/t Artem Klevtsov)
* `unlist.BibEntry` and `RelistBibEntry` now retains `@strings` and `mheader` and
`mfooter` attributes (see ?BibEntry) if they are present

Changes in Version 0.8.34 (2014-08-18)
--------------------------------------------------------

NEW FEATURES

* Added function `GetDOIs` which searches CrossRef for DOIs for the citations stored in
a `BibEntry` object

BUG FIXES

* `ReadCrossRef` fixed to account for change to CrossRef API endpoint. (h/t Carl Boettiger)
* Abstracts returned by NCBI Entrez can be multiple parts.  This is now handled correctly and the complete
abstract will be returned in the 'abstract' field. (h/t Erich Studerus)
* DOI's were too naively extracted from NCBI Entrez results, resulting in some entries having 'doi' fields with
length greater than one.  Now fixed. (h/t Erich Studerus)

Changes in Version 0.8.32 (2014-08-14)
--------------------------------------------------------

NEW FEATURES

* Functions for interacting with NCBI Entrez return abstract of each article (request of Erich Studerus)

BUG FIXES

* `print.BibEntry` with `BibOptions(style = "citation")` now works properly
* Examples calling web resources should no longer upset the check farm (h/t HI&RH Lord Ripley of England)


Changes in Version 0.8.3 (2013-07-30)
---------------------------------------------------------

NEW FEATURES

* `as.BibEntry` will create entry key if given a `bibentry` object with no key.  Useful when citing
packages with `citation`.
* PrintBibliography and Cite functions (Cite, Citet, etc.) accept `bibentry` objects in addition to
`BibEntry` objects.
* `$<-.BibEntry` will now accept a single person object, so that a single author in a multi-author entry
may be updated.  An example may be found at `help("$<-.BibEntry")`.  (h/t Carl Boettiger)

BUG FIXES

* validated html
* changed example for `WriteBib` that occasionally failed check

Changes in Version 0.8.2 (2013-06-01)
---------------------------------------------------------

BUG FIXES

* Cite functions work if a specified entry has no key.  Note that keys should always be provided for all entries as they  are required for all entries in a BibLaTeX bib file (h/t Carl Boettiger)
* Entries returned by Crossref that have entry type 'Data' which is not supported by default in BibLaTeX are converted to type 'Online' (h/t Carl Boettiger)
* Fix for `ReadGS` when argument `check.entries` is FALSE or "warn" (h/t Francisco Rodriguez Sanchez)
* Family names from Scholar in all caps are handled correctly in ReadGS

NEW FEATURES

* Functions for interacting with PubMed return language of each article (h/t Dale Steele)
* Added CITATION file
* Updated License to explicitly include GPL-2 and GPL-3

Changes in Version 0.8.1 (2013-03-09)
---------------------------------------------------------

BUG FIXES

* Fix for `names<-.BibEntry`
* Fix for `print.BibEntry` when entry has urldate field but no url field
* Corrections for some documentation typos
* Fix pmidrelated field when `batch.mode = FALSE` in `GetPubMedRelated`
* Fix for `LookupPubMedID` when `index` argument specified
* `open.BibEntry` now works properly
* Fix for converting thesis entries in `toBibtex.BibEntry`
* Fix for `WriteBib` with `biblatex` argument

NEW FEATURES

* Added Vignettes including user manual and Rmd citation examples
* Added NEWS
* Added HTML output of Rmd and RHTML citation examples to doc/
