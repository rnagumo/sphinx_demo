
# sphinx_demo

sphinxを使うためのメモ

# 1. 使い方

## 1.1 インストール

現在の環境にsphinx，及びテーマをインストールする．

```bash
pip install sphinx sphinx_rtd_theme
```

## 1.1 Quick start

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

## 1.2 conf.pyの書き換え

`docs/source/conf.py`内を書き換える．書き換える点は三箇所ある．

### 1.2.1 Path configuration

Pythonパッケージへのパスを記入する．

```python
import os
import sys
sys.path.insert(0, os.path.abspath('../../proj/'))
```

### 1.2.2 Extension for docstrings

Docstringsを読み込むためのextensionを追加する．

```python
extensions = ['sphinx.ext.autodoc', 'sphinx.ext.napoleon']
```

### 1.2.3 HTML theme

rtd themeと呼ばれるものが広く使われており，それをインポートする．

```python
import sphinx_rtd_theme
html_theme = 'sphinx_rtd_theme'
html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
```

## 1.3 rstファイルの作成

```bash
~/sphinx_demo/docs$ sphinx-apidoc -f -o ./source/ ../proj/
```
