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

  * `1.4`, `1.5`, `1.6`, `1.7` or `2.0`: Sets PDF version.
  * `nocompress`: Suppresses stream compression.
  * `compress` (default): Does not suppress stream compression.
  * `noobjcompress`: Suppresses use of object streams.
  * `objcompress` (default): Does not suppress use of object streams.
  * Driver options: As below:
      + When the new PDF management of LaTeX is activated, the package
        will automatically switch to “latex-pdf” mode. You need not
        give driver options.
      + When using a PDF-output engine, you need not give driver options
        since the appropriate one is auto-detected.
      + `dvipdfmx`: Uses dvipdfmx driver.
      + `nodvidriver`/`disabled`: Disables all functions of the package.  
        NB. This option sets `lenient+` by default.
  * `ignorepdfmanagement`: Avoids switching to “latex-pdf” mode, even
    when the new PDF management of LaTeX is activated.
  * `lenient`: Turns the errors for unsupported features into warnings.
  * `lenient+`: Suppreseses the errors for unsupported features.
  * `nolenient`: Negation of `lenient(+)`.

Note that the options `compress` and `objcompress` mean that this
package *does not suppress* a feature. They do not reactivate a feature
when it is already suppressed by other means.

### USAGE

  * `\setpdfversion{<version>}`: Sets PDF version.
    Here `<version>` is either one of the following:
      + `1.4`, `1.5`, `1.6`, `1.7` or `2.0`; the version itself.
      + the name of a PDF file; the version is set equal to that of
        the given file.
  * `\suppresspdfcompression`: Suppresses stream compression.
  * `\suppresspdfobjcompression`: Suppresses use of object streams.
  * `\setpdfdecimaldigits{<precision>}`: Sets the precision (the number
    of digits after decimal points) of the decimal numbers that appear
    in PDF command sequences.
  * `\preservepdfdestinations`: Stops shortening the PDF destination
    names and uses the original names given in the LaTeX documents. This
    is necessary for cross-document links to work correctly.
  * `\setpdfpkresolution{<resolution>}`: Sets the resolution (in dpi)
    of the PK fonts embedded in the PDF file.

### NOTE ON DRIVERS

           \ Drivers (engines)     pdfTeX     dvipdfmx
    Features                       / LuaTeX   / XeTeX    latex-pdf
    ---------------------------    ---------  ---------  ---------
    \setpdfversion                 Yes        Yes        Yes
    \suppresspdfcompression        Yes        Maybe(*2)  Yes(*4)
    \suppresspdfobjcompression     Yes        Maybe(*2)  Yes(*4)
    \setpdfdecimaldigits           Yes        Maybe(*2)  No
    \preservepdfdestinations       No-op(*1)  Maybe(*2)  No
    \setpdfpkresolution            Yes        Maybe(*3)  No

 1. In pdfTeX and LuaTeX, PDF destination names are never shortened;
    that is, it can be thought as if `\preservepdfdestinations` were
    always in effect.
 2. These features are available only when the version of (x)dvipdfmx
    is 20160307 or later.
 3. These features are available only when the version of (x)dvipdfmx
    is 20211016 or later.
 4. As for '\suppresspdfcompression' and '\suppresspdfobjcompression',
    when one of them is executed, the other will be activated. It is
    because l3pdf module does not support activating only one of them.

On the detection of dvipdfmx version:

  * Shell escape must be accepted (with or without restriction) so that
    `kpsewhich` and `extractbb` will be allowed to run, because those
    programs are used in order to detect the dvipdfmx version.
  * The detection process is slow, so the result is cached in the
    auxiliary file (`.aux`). When the environment is changed, you need
    to delete the auxiliary file.

More notices:

  * If you try to use unavailable features, an error will occur.  
    NB. Option `lenient` turns the errors into warnings, and `lenient+`
    completely suppresses the errors.
  * The package recognizes some “unsupported” driver options such as
    `dvips`; when such drivers are used, use of any feature will cause
    an error.
  * The use of `nodvidriver` sets `lenient+` by default; use of any
    feature will do nothing (nor issue an error).


REVISION HISTORY
----------------

  * Version 0.8a ‹2025/02/18›
      - Give up checking dvipdfmx version when the scratch extractbb
        is used.
  * Version 0.8  ‹2024/08/03›
      - Support some features even when the new PDF management of the
        LaTeX kernel is activated (“latex-pdf” mode).
  * Version 0.7  ‹2024/07/24›
      - Support (officialy) `\setpdfpkresolution`.
  * Version 0.6  ‹2022/04/28›
      - Added the `lenient+` and `nolenient` options.
  * Version 0.5a ‹2021/02/14›
      - Adjustment for the new version of hyperref.
  * Version 0.5  ‹2020/04/19›
      - Suuport PDF version value `2.0`.
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
