---
title: Emotion Analysis using Trees and Bi-LSTM with LIME Interpretability
subtitle: Decoding Emotions - Trees, Bi-LSTM, and LIME Unveiling the Sentiment Spectrum
summary: Embark on a journey into the realm of emotion analysis as we deploy decision trees and Bi-LSTM models to predict the sentiment of textual expressions. Witness the power of interpretability with LIME, shedding light on the intricate decisions made by our models. A fusion of traditional and advanced approaches achieves an 84% accuracy milestone, bringing us closer to understanding the emotional nuances encoded in language.
authors:
  - admin
tags: []
categories: []
projects: []
date: '2023-12-10T00:00:00Z'
lastMod: '2024-01-01T00:00:00Z'
image:
  caption: ''
  focal_point: ''
---

```python
from IPython.core.display import Image
Image('https://www.python.org/static/community_logos/python-logo-master-v3-TM-flattened.png')
```

![png](./index_1_0.png)

```python
print("Welcome to Academic!")
```

    Welcome to Academic!

## Install Python and JupyterLab

[Install Anaconda](https://www.anaconda.com/distribution/#download-section) which includes Python 3 and JupyterLab.

Alternatively, install JupyterLab with `pip3 install jupyterlab`.

## Create or upload a Jupyter notebook

Run the following commands in your Terminal, substituting `<MY-WEBSITE-FOLDER>` and `<SHORT-POST-TITLE>` with the file path to your Academic website folder and a short title for your blog post (use hyphens instead of spaces), respectively:

```bash
mkdir -p <MY-WEBSITE-FOLDER>/content/post/<SHORT-POST-TITLE>/
cd <MY-WEBSITE-FOLDER>/content/post/<SHORT-POST-TITLE>/
jupyter lab index.ipynb
```

The `jupyter` command above will launch the JupyterLab editor, allowing us to add Academic metadata and write the content.

## Edit your post metadata

The first cell of your Jupter notebook will contain your post metadata ([front matter](https://sourcethemes.com/academic/docs/front-matter/)).

In Jupter, choose _Markdown_ as the type of the first cell and wrap your Academic metadata in three dashes, indicating that it is YAML front matter:

```
---
title: My post's title
date: 2019-09-01

# Put any other Academic metadata here...
---
```

Edit the metadata of your post, using the [documentation](https://sourcethemes.com/academic/docs/managing-content) as a guide to the available options.

To set a [featured image](https://sourcethemes.com/academic/docs/managing-content/#featured-image), place an image named `featured` into your post's folder.

For other tips, such as using math, see the guide on [writing content with Academic](https://wowchemy.com/docs/content/writing-markdown-latex/).

## Convert notebook to Markdown

```bash
jupyter nbconvert index.ipynb --to markdown --NbConvertApp.output_files_dir=.
```

## Example

This post was created with Jupyter. The orginal files can be found at https://github.com/gcushen/hugo-academic/tree/master/exampleSite/content/post/jupyter
