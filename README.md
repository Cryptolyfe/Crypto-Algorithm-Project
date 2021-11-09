# Crypto-Algorithm-Project
Project 2
## Description
We are creating an algorithmic trading bot to predict the future price of Bitcoin and Ethereum using back data.  We will be using machine learning models to test the back data and risk/performance.  We will use QuantConnect to create our algorithm. 

## Research Question 
Can our algorithm beat the market by purchasing crypto when the currency price exceeds the deep learning model's forecasted price? 

## Datasets/Models 
We are using historical data for Bitcoin and Ethereum from Bitfinex and then training a NeuralNetworkAlgorithm to create trades based on the backtested data.  We are using the LSTM plus the standard deviation as a threshold for identifying trends.

## Task Breakdown 
Source code from https://github.com/QuantConnect/Lean/blob/master/Algorithm.Python/KerasNeuralNetworkAlgorithm.py
Compile back data for Bitcoin and Ethereum using Bitfinex and create a NeuralNetworkAlgorithm that accurately predicts future data. 

To begin, define the KerasNeuralNetworkAlgorithm. The KerasNeuralNetworkAlgorithm is an algorithm that inherits from the QCAlgorithm class.  It will be training
the model every monday to keep the model fresh and dynamic, while trading three times daily.
Attributes used for this are as follows:
self.lookback - trains the model based off of the past n days
self.modelBySymbol - a dictionary of models accessible by a symbol
self.window - the number of previous data points used to forecast a prediction
  
Then we define the initialize function with Start Date, Set type of account, Window, ModelbySymbol and Lookback for BTC and ETH
After this we set the Benchmark (BTCUSD) and train the model the first time with our NeuralNetworkTraining_new function
Following this we set the Neural network to train every Monday and scheduled it to trade 30 minutes after markets open in North America, Europe and Asia respectively

We use daily historical data to train our machine learning model and build a neural network form 1st to last layer using the LSTM model 
We then train the models
We created a new trade function based on the source code provided to predict the price using the trained model and out-of-sample data
Enter or exit positions are based on the relationship of the open price of the current bar (minutely) and the prices defined by the machine learning model.
Our algo enters a position if it doesn't have the position and if the current price broke the deep learning's predicited trend (plus 1 standard deviation)
our model liquidates if it has a position and the current price drops below the deep learning predicited trend(-1 standard deviation). 
we created a window_data function that accepts the column number for the features (X) and the target (y).
It chunks the data up with a rolling window of Xt - window to predict yt.
It returns two numpy arrays of X and y.
we converted the window data to tensors 
we built the neural network  for each stock this time changing LSTM, changing input_dim to input_shape, and giving it the correct shape


To further improve the model we could tune the model in a research notebook,
