# WSDM 2020
### Team name:SimpleBaseline
### Members: 
* Chi-Yu Yang 
    * Department of Computer Science and Information Engineering, National Taiwan University 
    * r08922a15@csie.ntu.edu.tw
* Kuei-Chun Huang 
    * Department of Computer Science and Information Engineering, National Taiwan University
    * r08922010@csie.ntu.edu.tw
### Data Leak:
we found that only using the first 45000 paper in candidate paper boosted our model from 0.34664257402658 to 0.414412839045621 on public leaderboard. Same on private leaderboard. We also tried 44000 and 47500 which worse than 45000. 
### prediction generating procedure
***
+ run `preprocess` cell (done)
+ run the following steps at the same time for testing data
    + recall
        + five kinds of recall
            + bm25: run `recall - BM25` cell 
            + idf: run `recall - idf` cell 
            + s2v: run `sent2vec_recall.ipynb` directly 
            + blue: run `sent_bert_blue.ipynb`  then run `bluebert_recall.ipynb`
            + key: run `keywords_recall.ipynb` directly
        + run the next three cells to merge all of them
    + embeddings for feature
        + `gen_vectors.ipynb`: get Word2Vec, FastText, and SIF 
        + `bert.ipynb`: get `description2embedding_pre.pkl`
        + `sent2vec_embedding.ipynb`: get `description2embedding_s2v.pkl` 
        + `sent_bert_sci.ipynb`: get `description2embedding.pkl` 
+ run super fat `get features` cell after the above are all done
+ run `lgb.ipynb` directly to get prediction