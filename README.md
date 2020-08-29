# Flipr_Hackathon
This is the solution for stock-market prediction problem given in flipr 5.0.
## The problem
The problem here is to predict stock market price from various relevant features. And also to do a time series modelling for predicting future put call ratio(which is a time dependent quantity).

## Time Series Modelling:
Here, I trained a RNN for time series prediction(part 2 in the given task) in a self supervised way!<br/>
We know that every data has some flaws and this data is not an exception. The data has some missing values in it. We can deal with the missing values by directly dropping them or filling them with some constant. But both these methods have their own disadvantages.<br/>
First one will effect the size of training data and in the later one, we are imposing a high error in missing values which might hurt our model's performace.
So I came up with a self supervised way of training which makes model to get an overview of data.<br/>

## My Idea for time series modelling:
   1. Building a dynamic RNN with dense layers on top of it.<br/>
   2. Now, this model takes sequence of length 5 of which we randomly make some elements zero(I have made 1 or 2 elements zero randomly) and a mask having 1's at the positions where we made zeros in the sequence and 0's at rest of the positions as inputs and output the a sequence of same length 5<br/>
   3. we will optimize the above built RNN to output a sequence of same length 5, having missing values.This concludes our pretraining part which is purely inspired from masked language modelling from field of Natural Language Processing.<br/>
   4. Now, we will take the pretrained model and remove the dense layers(which are on top of RNN) and retrain this model to predict put calls ratio on august 15th from the data of august 10th,11th,12th,14th.<br/>
    5. That's it! we are done with building a time series model which can predict put calls ratio by considering the values of prior 5 days.<br/>

Feel free to go through the below code to get to know about the additional information like hyperparemeters, architecture, etc.,.
