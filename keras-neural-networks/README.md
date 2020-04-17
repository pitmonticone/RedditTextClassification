{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Keras Neural Networks\n",
    "\n",
    "This folder contains three approaches with nueral networks.\n",
    "\n",
    "### 1. TFIDF classification\n",
    "\n",
    "This task is brought forward by the `simpleNet.ipynb`,`simpleNetPrediction.ipynb`,`simplenetgrid.ipynb`. The first validates the model, the third gridsearchs it and the fourth outpus the predictions. It does roc =  89.7 on the test set.\n",
    "\n",
    "### 2. Embeddings classification\n",
    "\n",
    "Trains and predicts an embedding layer before classifying. Several netowrks have been tried. Due to a poorer validation performance if compared to more transparent models like an MLP on doc2vec (see [successful-model](https://github.com/pitmonticone/data-mining-challange/tree/master/successful-models)), we thought it not to be worth a gridsearch & prediction effort.\n",
    "\n",
    "### 3. Embeddings classification\n",
    "\n",
    "Same as above, but with glove vectors pretrained on 6B words and 300 dimensions."
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "tf-gpu",
   "language": "python",
   "name": "tf-gpu"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.10"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
