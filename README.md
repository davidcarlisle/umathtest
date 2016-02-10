# umathtest

Test update of amsmath.sty so that it works with luatex 0.8x and to fix some other issues.


## Main Changes


### DOTSB change

adjust the initial check so that it accepts
\coprod reported as \mathchar or \Umathchar
luatex 0.89 reports \Umathchar even if the original
definition used \mathchardef

### \Umathch@ addition


### \thecharacter@ addition
detect catcode 12 characters (or implicit characters)
and look up (U) mathcode, Could also do this
with mathcode for 8bit tex but less useful there
so do nothing in that case for compatibility with previois
code.


### \long fix
remove "\long " from a \meaning string
in previous versions \long macros were not seen
bad as this file uses \(re)newcommand for \implies, \iff, \hookrightarrow etc.

### additional test for a catcode 12 character

### Mathstrut change

Original code assuming \mathcode is kept for 8bit TeX. Unicode TeX
uses \Umathcharnumdef which works for xetex and luatex, which use
different forms for \mathchardef. (New luatex always reports
definitions using \Umathchardef syntax even if \mathchardef used.)
%%
The u-tex version uses e-tex \fontcharht to avoid boxing which
could also be done for pdftex, but not done here.
Note that currently luatex-math package (imported by uniocde-math)
checks this definition before changing it so that package would need
an update here to avoid a spurious warning.

### mathaccent change

This just adjusts the test made at package load to recognise
\Umathaccent Although currently it is just used to give a
modified warning that the accents will not be redefined.

Note that the engines behave quite differently here, luatex
even without these definitions using the OpenType accent set up by
unicode-math  stacks \hat{hat{f}} correctly but xetex acts like
classic tex and needs this adjustment. This difference is not
addressed here at all.

This test is just at package loading and has no affect on the
definitions used in 8bt TeX.
