<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Project Status: Wip - Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](http://www.repostatus.org/badges/0.1.0/wip.svg)](http://www.repostatus.org/#wip) [![](http://www.r-pkg.org/badges/version/reprex)](http://www.r-pkg.org/pkg/reprex)

<!-- [![Build Status](https://travis-ci.org/jennybc/reprex.svg?branch=master)](https://travis-ci.org/jennybc/reprex) -->
### reprex

Prepare reproducible examples for posting to stackoverflow, github issues, etc.:

-   given R code on the clipboard or in a file
-   run it via `rmarkdown::render()`
-   with deliberate choices re: arguments and setup chunk
-   get resulting runnable code + output as markdown
-   formatted for target venue, e.g. `so` or `gh`
-   on the clipboard and/or in a file

#### Reproducible examples

What is a `reprex`? It's a {rep}roducible {ex}ample. Coined by Romain Francois [on twitter](https://twitter.com/romain_francois/status/530011023743655936).

Where and why are they used?

-   A stackoverflow question that includes a proper reprex is [much more likely to get answered](http://stackoverflow.com/help/no-one-answers), by the most knowledgeable and therefore busy people.
-   A [GitHub issue](https://guides.github.com/features/issues/) that includes a proper reprex is more likely to achieve your goals: getting a bug fixed, getting a new feature, in a finite amount of time.

Read the stackoverflow thread ["How to make a great R reproducible example?"](http://stackoverflow.com/questions/5963269/how-to-make-a-great-r-reproducible-example/16532098) to learn important guiding principles! That is NOT what this package is about. This package helps with the fiddly mechanics of preparing runnable bits of code for posting.

#### Philosophy

The reprex code:

-   Must run and, therefore, should be run **by the person posting**. No faking it.
-   Should be easy for others to digest, so **they don't necessarily have to run it**. We might include selected bits of output. :scream:
-   Should be easy for others to copy + paste + run, **iff they so choose**. Don't let inclusion of output break executability.

Accomplish this like so:

-   use `rmarkdown::render` or, under the hood, `knitr::spin` to run the code and capture output that would display in R console
-   use chunk option `comment = "#>"` to include the output while retaining executability

#### Formatting principles

Notes and links re: best formatting for different venues.

stackoverflow

-   <http://stackoverflow.com/editing-help>
-   specifics re: [code highlighting](http://stackoverflow.com/editing-help#syntax-highlighting)

github

-   github issues use github-flavored markdown

gist.github.com

-   In theory, this is the domain of [`gistr`](), but people also tend to post `.R` or `.Rmd` and NOT resulting `.md` ... is there a gap in tools or is this just a behavior?

#### Other work

The "great R reproducible example" stackoverflow thread referenced above has some discussion of practical details, such as [this comment](http://stackoverflow.com/questions/5963269/how-to-make-a-great-r-reproducible-example/16532098#16532098).

The "Code to import data from a Stack overflow query into R" [stackoverflow thread](http://stackoverflow.com/questions/10849270/code-to-import-data-from-a-stack-overflow-query-into-r/10849315). This is from the perspective of someone considering answering a question, in which the OP has not provided a proper reprex. Specifically: the input data is in suboptimal form.

The [github package `overflow`](https://github.com/sebastian-c/overflow/). Appears to also emphasize the difficulty above, e.g., getting data out of stackoverflow questions that don't follow reprex best practices. A bit hard to tell what's there, not much in README, no vignette.

#### notes parking

Clipboard stuff

-   sadly, implementation is very OS specific
-   The psych package has a function `read.clipboard()` that takes the OS into account. Not on github but gzipped tarballs of devel version available here, if I decide to take a look: <http://personality-project.org/r/src/contrib/>.
-   <http://stackoverflow.com/questions/9035674/r-function-to-copy-to-clipboard-on-mac-osx?lq=1>

Lines where a `.R` file gets spun in `render()`: [render.R\#L129-L154](https://github.com/rstudio/rmarkdown/blob/88afb8d4d6f4371d67b82059baaee1052d2bc55f/R/render.R#L129-L154)

A collection of R scripts by github user rsaporta contains some functions related to stackoverflow (note: there is no license on any of this): [so\_functions.r](https://github.com/rsaporta/pubR/blob/fe487d7020311b19b92d80e214800813188ad793/so_functions.r).
