# Deep Learning for Tabular data: A bag of tricks | OSDC2020
How to develop deep learning project for tabular data
[Link](https://www.youtube.com/watch?v=WPQOkoXhdBQ&t=332s)

## Preparation
- missing values: impute and new column
- categorical: one-hot
- test: tf-idf
- normalize
- cross validation
- benchmark with other models

## Design
- start with a low capacity net
- loss function
- activation function
	- output: rmse, rmsle, game, poisson, tweedy
	- hidden: sigmoide, softplus, tanh, swish, mish, relu, leakReLu

## Training
- batch size: Set the size to be about 1% of the dataset
	- small : difficult to converge to minima as gradients will dramatically change each iteration -> underfitting and slow training
	- large: tend to convert to sharp minima which leads to poor generalization -> overfitting and large memory usage 
- learning rate
	- LR range test
	- one-cycle-learning
- epochs for one cycle policy: start a few epochs(4) and find better epochs that better works

## Assessment
- compare prediction distribution to target distribution
- compare loss of training and validation
- Generalization error requires other data processing or feature selection 
- Examine confidence vs. confusion using binned probabilities, confusion matrix and calibration
- Compare with benchmark and consider why it performed better or worse
	- Very poor means: wrong with skip connection -> remove hidden layer and walking through our design steps like activation and loss functions
	- Not Bad means: proceed tuning
	- Worse than tree models: means a discontinuity like artificial clipping in the data or multimodal or overlapping distributions

## Tuning
### Dealing with discontinuities
- stack with a tree model
- training separate networks for each important split
- ensembling subset specialized networks(like forest)
- vary model size

### Batch norm
- Often dramatically improves binary classification
- Can be detrimental to regression

### Overfitting
- Increase learning rate
- decrease batch size
- increase weight decay
- fewer epochs
- reduce network size
- increase dropout

### Underfitting
- decrease learning rate
- increase batch size
- reduce weight decay
- more epochs
- larger network size
- reduce dropout
