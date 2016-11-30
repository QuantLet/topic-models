
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VisualTFIDF** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet : VisualTFIDF

Published in : Bachelor Thesis "Probabilistic Topic Models in Natural Language Processing"

Description : 'Plots index terms of large text corpora with respect to their document frequency in
the corpus'

Keywords : TFIDF, document frequency, Vector Space Model, text mining, Visualisation, bar chart

Author : Jerome Bau

Submitted : November 17 2016 by Jerome Bau

Input : tfidf corpus as created through the Python gensim libraries

```


### PYTHON Code:
```python
from gensim import models, corpora
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


class VisualTFIDF(object):
    """Visualizes a TF-IDF matrix as created through the gensim Python extension"""
    def __init__(self):
        self.tfidf = None
        self.tfidf_as_pd = None
        self.tfidf_as_pd_labeled = None
        self.id2word = None

    def load_tfidf(self, path):
        """Load a preprocessed saved tfidf matrix"""
        self.tfidf = models.TfidfModel.load(path)

    def load_dict(self, path):
        self.id2word = corpora.Dictionary.load_from_text(path)

    def make_pandas_vec(self):
        """ Make a pandas vector"""
        tf = self.tfidf.dfs
        idf = self.tfidf.idfs
        p = pd.concat([pd.Series(tf), pd.Series(idf)], axis=1)
        p.columns = ['df', 'idf']
        self.tfidf_as_pd = p

    def pandas_vec_add_labels(self):
        """Replace the id with the corresponding token"""
        ind = []
        for i in range(len(self.tfidf_as_pd)):
            ind.append(self.id2word[i])
        self.tfidf_as_pd_labeled = self.tfidf_as_pd
        self.tfidf_as_pd_labeled.index = pd.Series(ind)

    def barplot_term_frequencies(self, top):
        """Create a bar plot with descending term frequency for the top k terms"""
        od = np.arange(top)
        ordered_pd = self.tfidf_as_pd_labeled.sort_values('df', ascending=False)
        plt.bar(od, ordered_pd['df'][:top], align='center', alpha=0.4)
        # plt.xticks(od, ordered_pd.index[:top])
        plt.xticks([int(0.1 * top * i) for i in range(int(0.01 * top))],
                   [self.tfidf_as_pd_labeled.sort_values('df', ascending=False).index[int(0.1 * top * i)] for i in range(int(0.01 * top))], rotation=70)
        plt.ylabel('Number of documents')
        plt.show()

```
