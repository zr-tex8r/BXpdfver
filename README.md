BXpdfver Package
================

LaTeX: To specify the version and compression level of output PDF files

This package enables users to specify in their sources the following
settings on the PDF document to output:

  * PDF version (1.4, 1.5 etc.);
  * whether or not to compress streams;
  * whether or not to use object streams.
  * precision of decimal numbers used in PDF commands
  * whether or not to preserve (not shorten) PDF destination names

### SYSTEM REQUIREMENT

  * TeX format: LaTeX.
  * TeX engine: pdfTeX, XeTeX, LuaTeX, and any DVI-output engines.
  * DVI-ware (in DVI mode): dvipdfmx.
  * Required packages:
      - atbegshi (when using dvipdfmx driver)

### INSTALLATION

  - `*.sty` → $TEXMF/tex/latex/BXpdfver

### LICENSE

This package is distributed under the MIT license.

bxpdfver package
----------------

### PACKAGE LOADING

    \usepackage[<option>,...]{bxpdfver}

The available options are:

  * `1.4`, `1.5`, `1.6`, or `1.7`: Sets PDF version.
  * `nocompress`: Suppresses stream compression.
  * `compress` (default): Does not suppress stream compression.
  * `noobjcompress`: Suppresses use of object streams.
  * `objcompress` (default): Does not suppress use of object streams.
  * Driver options: As below:
      + When using a PDF-output engine, you need not give driver options
        since the appropriate one is auto-detected.
      + `dvipdfmx`: Uses dvipdfmx driver.
      + `disabled`/`nodvidriver`: Disables all functions of the package.
  * `lenient`: Turns the errors for unsupported features into warnings.

Note that the options `compress` and `objcompress` mean that this
package *does not suppress* a feature. They do not activate a feature
when it is already suppressed by other means.

### USAGE

  * `\setpdfversion{<version>}`: Sets PDF version.
    Here `<version>` is either one of the following:
      + `1.4`, `1.5`, `1.6`, or `1.7`; the version itself.
      + the name of a PDF file; the version is set equal to that of
        the given file.
  * `\suppresspdfcompression`: Suppresses stream compression.
  * `\suppresspdfobjcompression`: Suppresses use of object streams.
  * `\setpdfdecimaldigits{<precision>}`: Sets the precision (the number
    of digits after decimal points) of the decimal numbers that appear
    in PDF command sequences.
  * `\preservepdfdestinations`: Stops shortening the PDF destination
    names and uses the original names given in the TeX documents. This
    is necessary for cross-document links to work correctly.

### NOTE ON DRIVERS

           \ Drivers (engines)     pdfTeX     dvipdfmx
    Features                       / LuaTeX   / XeTeX    others
    ---------------------------    ---------  ---------  ------
    \setpdfversion                 Yes        Yes        No
    \suppresspdfcompression        Yes        Maybe(*2)  No
    \suppresspdfobjcompression     Yes        Maybe(*2)  No
    \setpdfdecimaldigits           Yes        Maybe(*2)  No
    \preservepdfdestinations       No-op(*1)  Maybe(*2)  No

 1. In pdfTeX and LuaTeX, PDF destination names are never shortened;
    that is, it can be thought as if `\preservepdfdestinations` were
    always in effect.
 2. These features are available only when the version of (x)dvipdfmx
    is 20160307 or later. Also shell escape must be accepted (with or
    without restriction) so that `kpsewhich` and `extractbb` will be
    allowed to run, because those programs are used in order to detect
    the dvipdfmx version.

More notices:

  * If you try to use unavailable features, an error will occur.
  * The package recognizes some “unsupported” driver options such as
    `dvips`; when such drivers are used, use of any feature will cause
    an error.
  * When `disabled` is used, use of any feature will do nothing (nor
    issue an error).

REVISION HISTORY
----------------

  * Version 0.4  ‹2017/02/11›
      - Add `\setpdfdecimaldigits` and `\preservepdfdestinations`.
  * Version 0.3  ‹2016/08/11›
      - Supported all features on dvipdfmx/XeTeX.
  * Version 0.2b ‹2016/08/10›
      - Added the `lenient` option.
      - Supported the newer version of LuaTeX.
  * Version 0.2a ‹2015/08/05›
      - Minor fix.
  * Version 0.2  ‹2014/07/04›
      - First public version.

--------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r
