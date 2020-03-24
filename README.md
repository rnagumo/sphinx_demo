
# sphinx_demo

sphinxを使うためのメモ

# 1. Docsの作成

## 1.1 インストール

現在の環境にsphinx，及びテーマをインストールする．

```bash
pip install sphinx sphinx_rtd_theme
```

## 1.2 Quick start

まず，プロジェクトに`docs`ディレクトリを作る．

```bash
~/sphinx_demo$ mkdir docs
```

`docs`ディレクトリ内でSphinxプロジェクトを開始する．

```bash
~/sphinx_demo$ cd docs
~/sphinx_demo/docs$ sphinx-quickstart
```

最初の質問にはyesと答える（デフォルトはno）．あとは，プロジェクト名や著者名を適当に回答する．

```bash
> ソースディレクトリとビルドディレクトリを分ける（y / n） [n]: y
```

## 1.3 conf.pyの書き換え

`docs/source/conf.py`内を書き換える．書き換える点は三箇所ある．

### 1.3.1 Path configuration

Pythonパッケージへのパスを記入する．

```python
import os
import sys
sys.path.insert(0, os.path.abspath('../../proj/'))
```

### 1.3.2 Extension for docstrings

Docstringsを読み込むためのextensionを追加する．

```python
extensions = ['sphinx.ext.autodoc', 'sphinx.ext.napoleon']
```

### 1.3.3 HTML theme

rtd themeと呼ばれるものが広く使われており，それをインポートする．

```python
import sphinx_rtd_theme
html_theme = 'sphinx_rtd_theme'
html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
```

## 1.4 rstファイルの作成

ドキュメントの構成を表すrstファイルを`docs/source/`内に作成する．以下で，一つ目の引数はrstファイルの出力先を，二つ目の引数はPythonパッケージのフォルダを表す．

```bash
~/sphinx_demo/docs$ sphinx-apidoc -f -o ./source/ ../proj/
```

## 1.5 htmlファイルの作成

上述のコマンドで生成されたrstファイルを使い，htmlファイルを出力する．用意されているmake.batファイルを使用する．これによりHTMLファイルが作成されるので，所望の形になるまで編集を続ける．

```bash
~/sphinx_demo/docs$ make html
```

## 1.6 .gitignoreの編集

デフォルトのSphinxの設定では，`docs/build/`フォルダ内にHTMLファイルが作成される．しかし，Pythonのデフォルトの.gitignoreでは，buildフォルダを無視する．よって，docs/buildフォルダのみはバージョン管理に加えたいので，`!docs/build/`を追加する．

## 1.7 index.htmlの作成

GitHub Pagesは，`docs/`フォルダ内の`index.html`の存在を要求する．よって，`docs/`フォルダ内に`index.html`を作成し，以下の内容を記述する（[参考](https://github.com/sphinx-doc/sphinx/issues/3382#issuecomment-409068915)）．

```html
<meta http-equiv="refresh" content="0; url=./_build/html/index.html" />
```

## 1.8 GitHubへのpush

ここまででローカルの編集は終了である．GitHubのレポジトリにpushする．

## 2. GitHubの設定
