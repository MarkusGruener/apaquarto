# A Quarto Extension for Creating APA 7 Style Documents


<img loading="lazy" alt="any text: you like" src="https://img.shields.io/badge/lifecycle-experimental-orange">

This article template creates [APA Style 7th Edition
documents](https://apastyle.apa.org/) in .docx, .html. and .pdf.

If you want to type in markdown to create a document in the APA 6th
Edition format, I suggest using
[papaja](https://frederikaust.com/papaja_man/).

If you need all the flexibility of $\LaTeX$, I suggest using the [apa7
document class](https://ctan.org/pkg/apa7) with knitr and the [.Rnw
format](https://support.posit.co/hc/en-us/articles/200552056-Using-Sweave-and-knitr).

## Creating a New Article

To create a new article using this format, run this command in the
terminal:

``` bash
quarto use template wjschne/apaquarto
```

In RStudio, the terminal is a tab next to the console. If you cannot see
a terminal tab next to the console, use the keyboard shortcut
Alt-Shift-R to make a terminal appear.

Entering the command above will prompt a question about whether you
trust the author of the extension to not run malicious code. If you
answer Yes, you will be prompted to name a new folder where the
extension will be installed with an example document with the name of
the folder and a file extension of .qmd. The example document has most
of the instructions you will likely need.

## Using with an Existing Document

To add this format to an existing document:

``` bash
quarto add wjschne/apaquarto
```

Then, add the format to your document options:

``` yaml
format:
  apaquarto-docx: default
```

When adding this extension to an existing document, you will need to add
this line to the document right after its YAML metadata: (Note: The
[include statement](https://quarto.org/docs/authoring/includes.html)
needs to be surrounded by empty lines.)

``` markdown

{{{< include _extensions/wjschne/apaquarto/_apa_title.qmd >}}}
```

Here is an example of what the YAML metadata and the “include” statement
below it might look like:

    ---
    title: "My Paper's Title: A Full Analysis of Everything"
    shorttitle: "My Paper's Title"
    author:
      - name: W. Joel Schneider
        corresponding: true
        orcid: 0000-0002-8393-5316
        email: schneider@temple.edu
        affiliations:
          - name: Temple University
            department: College of Education and Human Development
            address: 358 Ritter Hall
            city: Philadelphia
            region: PA
            postal-code: 19122-6091
    abstract: "This is my abstract."
    keywords: [keyword1, keyword2]
    author-note:
      disclosures:
        conflict of interest: The author has no conflict of interest to declare.
    bibliograpy: mybibfile.bib     
    format:
      apaquarto-docx: default
    ---

    {{< include _extensions/wjschne/apaquarto/_apa_title.qmd >}}

## Example

This sample document has a fuller set of parameters specified and
contains instructions for formatting figures, tables, cross-references,
and more: [template.qmd](template.qmd).

The manuscript form in docx look like this:

![Preview of .docx output](img/docx.png)

The .html and .pdf output (in manuscript mode) look similar. The .pdf in
journal mode looks like this:

![Preview of .docx output](img/journalmode.png)

## Known Problems

- In apaquarto-pdf documents, getting tables work in `jou` mode for can
  be tricky. The problem is that any output that uses the `longtable`
  environment will not work in `twocolumn` mode. My solution is a bit
  hacky—I redefined `longtable` to use `supertablular` instead. This
  works in simple cases but undercuts some of `longtable`’s functions.
- In apaquarto-html documents, plain markdown tables do not render to
  APA format.
