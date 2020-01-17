# WSDM 2019
#### Team name: SimpleBaseline
* All codes were based on xiong's, first place of a similar competition few months ago.
### Members
***
* Chi-yu Yang 
    * Department of Computer Science and Information Engineering, National Taiwan University 
    * r08922a15@csie.ntu.edu.tw
* Kuei-chun Huang 
    * Department of Computer Science and Information Engineering, National Taiwan University
    * r08922010@csie.ntu.edu.tw
### Data Leak
***
In training data we found that there are around 90% of correct citations having no content in journal. Even more exciting thing is that the number of papers without content in journal is less than 35k, which is far less than the total number of papers! We thus dropped all papers having content in journal and made our first try, but the score turned out to be a big ZERO. Unbelievable as the result was, we could at least assume that there’s no correct citation without content in journal! By the way, due to the totally different distributions between training data and testing data we judged the quality of recall by recalling rate of papers having content in journal instead of all of them in training data.

After two weeks of development of recalling method and feature engineering, our score stuck at about 0.313. We used five different recalling approaches and prepared over 200 features, which we thought should not be too far away from score of top teams (0.337) if we didn’t have additional information. With last terrible experience we tried to drop papers with or without content in other attributes. Fortunately our score dramatically increased (0.345) when we drop papers without year. By these two successes we could have great confidence to claim that our recalling method and features had been robust enough for this task.

However, the excitement only last for a few hours then a team hit a despairing score, 0.379, at when we had dropped anything we could drop! All we could do was improving our recalling approaches. But unfortunately with three days of struggling, we could improve our performance just by a little bit and there was only two days left before the closing time. Since running recalling code was super time-consuming and we did not have too much time, we decided to cut the size of candidates to 50k to be able to try more parameters in our recalling algorithms. Surprisingly, the overall recalling rate dropped to the rate it supposed to be while the recalling rate of papers having content in journal was still unreasonably high! We then easily reached 0.400 by only keeping 50k papers as candidates. 

Finally by narrowing down to 45k we got 0.414 to be the first place on public leaderboard. Also on private leaderboard we got similar score, 0.417, which was surpassed by almost 0.01 a few hours before the closing time.

### prediction generating procedure
***
+ run `preprocess` cell
    + preprocess raw data
+ do the following steps for testing data
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
    + for predicting with trained lgb, run `lgb_old.ipynb` after modifying `n` and `paper_thd` with respect to the right input files