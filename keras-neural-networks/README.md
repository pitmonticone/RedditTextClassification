## Keras Neural Networks

This folder contains three approaches with nueral networks.

### 1. TFIDF classification

This task is brought forward by the `simple-net.ipynb`,`simple-net-prediction.ipynb`,`simple-net-grid.ipynb`. The first validates the model, the third gridsearchs it and the fourth outpus the predictions. It does roc =  89.7 on the test set.

### 2. Embeddings classification

Trains and predicts an embedding layer before classifying. Several netowrks have been tried. Due to a poorer validation performance if compared to more transparent models like an MLP on doc2vec (see [successful-models](https://github.com/pitmonticone/data-mining-challange/tree/master/successful-models)), we thought it not to be worth a gridsearch & prediction effort. Releted notebook: `embeddings.ipynb`

### 3. Embeddings classification

Same as above, but with glove vectors pretrained on 6B words and 300 dimensions. Releted notebook: `pretrained-embeddings.ipynb`
