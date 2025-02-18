BXpdfver パッケージバンドル
===========================

LaTeX: 出力 PDF のバージョンや圧縮状態を指定する

LaTeX 文書を PDF 文書に変換する際に出力 PDF に関する以下の設定を文書中で
行う機能を提供する。

  * PDF バージョン（1.4, 1.5 等）
  * ストリームの圧縮の有無
  * オブジェクトストリームの使用の有無

### 前提環境

  * フォーマット： LaTeX
  * エンジン： pdfTeX、XeTeX、LuaTeX、および DVI 出力のエンジン
  * DVIウェア（DVI出力時）： dvipdfmx
  * 依存パッケージ：
      - atbegshi（dvipdfmx ドライバの場合）

### インストール

  - `*.sty` → $TEXMF/tex/latex/BXpdfver

### ライセンス

本パッケージは MIT ライセンスの下で配布される。


bxpdfver パッケージ
-------------------

### パッケージ読込

    \usepackage[<オプション>,...]{bxpdfver}

利用可能なオプションは以下の通り。

  * `1.4`、`1.5`、`1.6`、`1.7`、`2.0`： PDF バージョンを指定する。
  * `nocompress`： ストリームの圧縮を抑止する。
  * `compress`（既定）： ストリームの圧縮を抑止しない。
  * `noobjcompress`： オブジェクトストリームの使用を抑止する。
  * `objcompress`（既定）： オブジェクトストリームの使用を抑止しない。
  * ドライバオプション： 以下の通り。なお、後述の「ドライバ指定」の
    節も参照されたい。
      + LaTeX の新 PDF マネジメントが有効化されている場合は、自動的に
        “latex-pdf”モードに切り替わる。ドライバオプションは不要である。
      + PDF 出力のエンジンの場合は、自動的に適切なドライバが選択される
        のでドライバオプションは不要である。
      + `dvipdfmx`： dvipdfmx 用のドライバを指定する。
      + `nodvidriver`／`disabled`： 全ての機能を無効化する。  
        ※この場合 `lenient+` が既定になる。
  + `ignorepdfmanagement`： “latex-pdf”モードへの切替を抑止する。
  * `lenient`： サポートしない機能に対するエラーを警告に格下げする。
  * `lenient+`： サポートしない機能に対するエラーを完全に抑止する。
  * `nolenient`（既定）： `lenient(+)` の否定。  
  * `new-dvipdfmx`： dvipdfmx に対するバージョン検査を省略し、常に最新の
    バージョンであると仮定する。  
    ※ドライバオプションが `dvipdfmx` に変更される。

`compress`、`objcompress` はこのパッケージによる抑止を行わないという意味
であり、既に抑止されている場合にそれを再び有効化するものではない。

### 機能

  * `\setpdfversion{<バージョン>}`： 出力 PDF バージョンを指定する。
    `<バージョン>` には以下の何れかを指定する。
      + `1.4`、`1.5`、`1.6`、`1.7`、`2.0` の何れか。その値に設定する。
      + PDF ファイルの名前。そのファイルのバージョンと同じ値に設定する。
  * `\suppresspdfcompression`： ストリームの圧縮を抑止する。
  * `\suppresspdfobjcompression`： オブジェクトストリームの使用を抑止
    する。（実はこの指定自体は圧縮とは無関係であるが、pdfTeX エンジンの
    プリミティブ `\pdfobjcompresslevel` に合わせた命令名を用いた。）
  * `\setpdfdecimaldigits{<精度>}`： PDF 命令列中に現れる小数値の精度
    （小数点以下の桁数）を指定する。
  * `\preservepdfdestinations`： PDF 目的地（PDF destination）の名前の
    短縮を抑止し、TeX 文書で指定された名前を用いる。異なる PDF 文書間で
    のリンクを正常に機能させるために必要である。
  * `\setpdfpkresolution{<解像度>}`： PDF に埋め込まれる PK フォントの
    解像度（dpi 値）を指定する。

### ドライバ指定に関する補足

           \ Drivers (engines)     pdfTeX     dvipdfmx
    Features                       / LuaTeX   / XeTeX    latex-pdf
    ---------------------------    ---------  ---------  ---------
    \setpdfversion                 Yes        Yes        Yes
    \suppresspdfcompression        Yes        Maybe(*2)  Yes(*4)
    \suppresspdfobjcompression     Yes        Maybe(*2)  Yes(*4)
    \setpdfdecimaldigits           Yes        Maybe(*2)  No
    \preservepdfdestinations       No-op(*1)  Maybe(*2)  No
    \setpdfpkresolution            Yes        Maybe(*3)  No

 1. pdfTeX／LuaTeX では PDF 目的地の名前が短縮されるることはない。つまり
    `\preservepdfdestinations` は常に有効になっていると見なせる。
 2. (x)dvipdfmx のバージョンが 20160307 以上である必要がある。
 3. (x)dvipdfmx のバージョンが 20211016 以上である必要がある。
 4. `\suppresspdfcompression` と `\suppresspdfobjcompression` については
    一方を実行すると他方も自動的に有効になる。l3pdf モジュールで片方のみ
    を有効化することはサポートされないからである。

dvipdfmx のバージョン判定について：

  - 必要が生じた場合にのみバージョン判定が実行される。
  - `new-dvipdfmx` オプションを指定した場合は、バージョン判定を全て
    省略した上で、最新の dvipdfmx を使用していると見なす。
  - バージョン判定のために kpsewhich と extractbb の起動を利用するため、
    少なくともこれらのプログラムについて、シェル実行が許可されている
    必要がある。
  - バージョン判定は少し時間がかかるため、dvipdfmx のバージョン情報は
    補助ファイル（.aux）中にキャッシュされる。このため、何か状況が変化
    した場合は、一旦補助ファイルを削除する必要が生じる。

以下のことにも注意されたい。

  * 使用不可能な機能を使おうと試みるとエラーが発生する。  
    ※`lenient` オプションが指定された場合はエラーが警告に変更され、
    また `lenient+` が指定された場合はエラーも警告も抑止される。
  * `dvips` 等の“全く対応していない”若干のドライバオプションを認識
    する。この場合、全ての機能の呼出でエラーが発生する。
  * `nodvidriver` オプションは既定で `lenient+` を指定する。つまり、
    どの機能の呼出でもエラーは発生しないが、全く何の動作も行わない。


更新履歴
--------

  * Version 0.8a ‹2025/02/18›
      - 新実装の extractbb が使われている場合は, dvipdfmx のバージョン
        検査を取りやめる。
  * Version 0.8  ‹2024/08/03›
      - カーネルの新 PDF マネジメントが有効な場合にも一部の機能が使える
        ようにする（“latex-pdf”モード）。
  * Version 0.7  ‹2024/07/24›
      - `\setpdfpkresolution` を（正式に）サポート。（dvipdfmx/XeTeX
        でも使用可能になった。）
  * Version 0.6  ‹2022/04/28›
      - `lenient+`/`nolenient` オプションを追加。
      - 非サポートのドライバでも読込自体はエラーにしない。
  * Version 0.5a ‹2021/02/14›
      - 新しい版の hyperref のための調整。
  * Version 0.5  ‹2020/04/19›
      - PDF バージョンの値として `2.0` をサポートする。
  * Version 0.4  ‹2017/02/11›
      - `\setpdfdecimaldigits`、`\preservepdfdestinations` を追加。
  * Version 0.3  ‹2016/08/11›
      - dvipdfmx/XeTeX でも全ての機能がサポートされる。
  * Version 0.2b ‹2016/08/10›
      - `lenient` オプションを追加。
      - 新しい LuaTeX エンジンのサポート。
  * Version 0.2a ‹2015/08/05›
      - 細かい修正。
  * Version 0.2  ‹2014/07/04›
      - 最初の公開版。

--------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r
