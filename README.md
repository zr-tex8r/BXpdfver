BXpdfver Package
================

LaTeX: To specify the version and compression level of output PDF files

This package enables users to specify in their sources the following
settings on the PDF document to output:

  * PDF version (1.4, 1.5 etc.);
  * whether or not to compress streams;
  * whether or not to use object streams.

### SYSTEM REQUIREMENT

  * TeX format: LaTeX.
  * TeX engine: pdfTeX, XeTeX, LuaTeX, and any DVI-output engines.
  * DVI-ware: dvipdfmx.
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
  * `compress` (defalt): Does not suppress stream compression.
  * `noobjcompress`: Suppresses use of object streams.
  * `objcompress` (default): Does not suppress use of object streams.
  * Driver options: As below:
      + When using a PDF-output engine, you need not give driver options
        since the appropriate one is auto-detected.
      + `dvipdfmx`: Uses dvipdfmx driver.
      + `disabled`: Disables all functions of the package.

Note that the options `compress` and `objcompress` mean that this
package *does not suppress* a feature. They do not active a feature
when it is already suppressed by other means.

### NOTE ON DRIVERS

  * pdfTeX and LuaTeX support all features.
  * XeTeX and dvipdfmx support only PDF version setting.
  * If you try to use unavailable features, an error will occur.
  * The package recognizes some “unsupported” driver options such as
    `dvips`; when such drivers are used, use of any feature will cause
    an error.
  * When `disabled` is used, use of any feature will do nothing (nor
    issue an error).

### COMMANDS

  * `\setpdfversion{<version>}`: Sets PDF version.
    Here `<version>` is either one of the following:
      + `1.4`, `1.5`, `1.6`, or `1.7`; the version itself.
      + the name of a PDF file; the version is set equal to that of
        the given file.
  * `\suppresspdfcompression`: Suppresses use of object streams.
  * `\suppresspdfobjcompression`: Suppresses use of object streams.

REVISION HISTORY
----------------

  * Version 0.2a [2015/08/05]
      - Minor fix.
  * Version 0.2  [2014/07/04]
      - First public version.

--------------------
Takayuki YATO (aka. "ZR")  
http://zrbabbler.sp.land.to/
