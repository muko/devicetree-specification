<!-- # Document master project for the Devicetree Specification # -->
# デバイスツリー仕様のドキュメントマスタープロジェクト

<!-- The latest release of the specification can be found at http://devicetree.org/specifications/ or https://github.com/devicetree-org/devicetree-specification/releases -->
仕様の最新リリースは、 http://devicetree.org/specifications/ または https://github.com/devicetree-org/devicetree-specification/releases にあります。 

<!-- This [repository](https://github.com/devicetree-org/devicetree-specification) holds the source for the generation of the Devicetree Specification using Sphinx and LaTeX.  -->
この[リポジトリ](https://github.com/devicetree-org/devicetree-specification)には、SphinxとLaTeXを使用してデバイスツリー仕様を生成するためのソースが保管されています。

<!-- ## Mailing list: devicetree-spec@vger.kernel.org ## -->
## メーリングリスト: devicetree-spec@vger.kernel.org ##
   <!-- * Use this mailing list for submitting patches, questions and general discussion -->
   * このメーリングリストを使用して、パッチ、質問、および一般的なディスカッションを送信してください 
   <!-- * Sign up to the mailing list at http://vger.kernel.org/vger-lists.html#devicetree-spec -->
   * http://vger.kernel.org/vger-lists.html#devicetree-spec でメーリングリストにサインアップします

## Build Instructions [![ci](https://github.com/devicetree-org/devicetree-specification/actions/workflows/ci.yml/badge.svg)](https://github.com/devicetree-org/devicetree-specification/actions/workflows/ci.yml) ##

Requirements:
* Sphinx: http://sphinx-doc.org/contents.html
 * version 1.2.3 or later
* LaTeX (and pdflatex, and various LaTeX packages)
* Graphviz (in particular, "dot"): http://www.graphviz.org/

On Debian and Ubuntu:

>```
># apt-get install python-sphinx texlive texlive-latex-extra libalgorithm-diff-perl \
>                  texlive-humanities texlive-generic-recommended graphviz \
>                  texlive-generic-extra
>```
>
>If the version of python-sphinx installed is too old, then an additional
>new version can be installed with the Python package installer:
>
>```
>$ apt-get install python-pip
>$ pip install --user --upgrade Sphinx
>$ export SPHINXBUILD=~/.local/bin/sphinx-build
>```
>
>You will need latexdiff v1.2.1 or later to create the changebars PDF version
>of the document.
>Until distributions catch up with the latest release you will need to install
>it directly from the github repo.
>
>```
>$ git clone https://github.com/ftilmann/latexdiff
>$ export PATH=$PWD/latexdiff/:$PATH
>```
>
>Export SPHINXBUILD (see above) if Sphinx was installed with pip --user, then follow Make commands below

On Mac OS X:

> Install [MacTeX](http://tug.org/mactex/)
>
> Install pip if you do not have it:
>```
>$ sudo easy_install pip
>```
>Install Sphinx
>```
>pip install --user --upgrade Sphinx
>Or
>sudo pip install --upgrade Sphinx
>```
>
>If you are using [brew](http://brew.sh) then you can install graphviz like this:
>```
>brew install graphviz
>```
>If you are using [macports](https://www.macports.org/) then you can install graphviz like this:
>```
>$ sudo port install graphviz
>```

Make commands:

>```
>$ make latexpdf # For generating pdf
>$ make html # For generating a hierarchy of html pages
>$ make singlehtml # For generating a single html page
>```

Output goes in ./build subdirectory.

..
    ## License ##
## ライセンス ##
..
    This project is licensed under the Apache V2 license. More information can be found 
    in the LICENSE and NOTICE file or online at:
このプロジェクトは、Apache V2 ライセンスの下でライセンスされています。
詳細については、LICENSE および NOTICE ファイルまたはオンラインの次の場所にあります。

http://www.apache.org/licenses/LICENSE-2.0

## Contributions ##
..
    Please submit all patches to the mailing list devicetree-spec@vger.kernel.org.
    Contributions to the Devicetree Specification are managed by the gatekeepers,
    Grant Likely <grant.likely@secretlab.ca> and Rob Herring <robh@kernel.org>
すべてのパッチをメーリングリスト devicetree-spec@vger.kernel.org に送信してください。
デバイスツリー仕様への貢献は、ゲートキーパーである Grant Likely <grant.likely@secretlab.ca> と Rob Herring <robh@kernel.org> によって管理されています。

..
    Anyone can contribute to the Devicetree Specification. Contributions to this project should conform 
    to the `Developer Certificate of Origin` as defined at http://elinux.org/Developer_Certificate_Of_Origin. 
    Commits to this project need to contain the following line to indicate the submitter accepts the DCO:
誰でもデバイスツリー仕様に貢献できます。
このプロジェクトへの貢献は、 http：//elinux.org/Developer_Certificate_Of_Origin で定義されている `Developer Certificate of Origin` に準拠している必要があります。
このプロジェクトへのコミットには、送信者が DCO を受け入れることを示す次の行を含める必要があります。
```
Signed-off-by: Your Name <your_email@domain.com>
```
..
    By contributing in this way, you agree to the terms as follows:
このように貢献することにより、次の条件に同意したことになります。
```
Developer Certificate of Origin
Version 1.1

Copyright (C) 2004, 2006 The Linux Foundation and its contributors.
660 York Street, Suite 102,
San Francisco, CA 94110 USA

Everyone is permitted to copy and distribute verbatim copies of this
license document, but changing it is not allowed.


Developer's Certificate of Origin 1.1

By making a contribution to this project, I certify that:

(a) The contribution was created in whole or in part by me and I
    have the right to submit it under the open source license
    indicated in the file; or

(b) The contribution is based upon previous work that, to the best
    of my knowledge, is covered under an appropriate open source
    license and I have the right under that license to submit that
    work with modifications, whether created in whole or in part
    by me, under the same open source license (unless I am
    permitted to submit under a different license), as indicated
    in the file; or

(c) The contribution was provided directly to me by some other
    person who certified (a), (b) or (c) and I have not modified
    it.

(d) I understand and agree that this project and the contribution
    are public and that a record of the contribution (including all
    personal information I submit with it, including my sign-off) is
    maintained indefinitely and may be redistributed consistent with
    this project or the open source license(s) involved.
```

<!-- SPDX-License-Identifier: Apache-2.0 -->
