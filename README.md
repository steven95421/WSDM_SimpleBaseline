# WSDM 2020
### Team name:SimpleBaseline
### Members: 
#### Chi-Yu Yang 

### prediction generating procedure
***
+ run `preprocess` cell (done)
+ run the following steps at the same time for testing data
    + recall
        + five kinds of recall
            + bm25: run `recall - BM25` cell (done)
            + idf: run `recall - idf` cell (done)
            + s2v: run `sent2vec_recall.ipynb` directly (done)
            + blue: run `sent_bert_blue.ipynb` in hpcuda then run `bluebert_recall.ipynb` directly (done)
            + key: run `keywords_recall.ipynb` directly (done)
        + run the next three cells to merge all of them
    + embeddings for feature
        + `gen_vectors.ipynb`: get Word2Vec, FastText, and SIF (done)
        + `bert.ipynb`: get `description2embedding_pre.pkl` (done)
        + `sent2vec_embedding.ipynb`: get `description2embedding_s2v.pkl` (done)
        + `sent_bert_sci.ipynb`: get `description2embedding.pkl` (done)
+ run super fat `get features` cell after the above are all done
+ run `lgb.ipynb` directly to get prediction