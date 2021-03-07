# What is overfitting? 

- [Motivation (What is overfitting?)](#motivation)
- [How can we tell?](#how-do-we-know)
- [What can we do?](#what-can-we-do)

## Motivation

If you have ever fitted a model, you probably remember that one time you tried again and again just for that last data point to fall on the line. Admit it, we’ve all been there, trying to make our model as "perfect" as possible. However, this is in fact dangerous. It could lead to what is called “overfitting”, and is not something to be encouraged. 

Let’s take a look at sample dataset below. Naturally, an intuitive model would be a curve that runs through the data points like this. <br> 
<img src="https://raw.github.ubc.ca/MDS-2020-21/DSCI_542_lab2_mmyz/master/img/points.png?token=AAAAJ7K26HS56RBBRIVEDD3AJVVA4" width="250">
<img src="https://raw.github.ubc.ca/MDS-2020-21/DSCI_542_lab2_mmyz/master/img/fit1.png?token=AAAAJ7JJKJQ6NLKQPPHZIA3AJVU6C" width="270">

However, you might feel a little uncomfortable with that last data point, so you refitted the model with a higher degree to accommodate that. 

<img src="https://raw.github.ubc.ca/MDS-2020-21/DSCI_542_lab2_mmyz/master/img/fit2.png?token=AAAAJ7KZRYYMNHVY2YBGNJLAJVVIU" width="270">

Now we have our model much more tailored to our dataset. If we keep accommodating every single data point, we might end up with something like this:

<img src="https://raw.github.ubc.ca/MDS-2020-21/DSCI_542_lab2_mmyz/master/img/fit3.png?token=AAAAJ7IFXNFQ4CI7Q5XUTW3AJVVKA" width="270">

It looks like a “perfect” model for our dataset, doesn’t it? Well… consider these new data points, which come from the same population but just weren't included in our initial dataset. How did our model appear to do? 

<img src="https://raw.github.ubc.ca/MDS-2020-21/DSCI_542_lab2_mmyz/master/img/preds.png?token=AAAAJ7MPJC6DXOX7T6324PTAJVVLY" width="270">

Not so well is it? We have essentially tailored our model specifically to the existing dataset at hand (yellow points). Our model learned not only the overall trend, but also the detail and noise among the yellow points. So when we collect any additional data (blue points), this model does a bad job in predicting the new data because it is tailored to describe the yellow points only, rather than the genuine trend of the data points. This is the idea of overfitting.

## How Do We Know?

Let’s now formally define `Overfitting`. The key question here is that: *When do we know it overfits?* While it seems to be a subjective question that varies from study to study, we can come up with a generalized way to measure the degree to which a model overfits. That is, to measure the difference between the errors within our dataset and the errors outside of our dataset. 

Let's refer back to our simple example above. When we overfitted, there was little error with our model on the yellow points (remember how all the yeollow points laid on the overfitted model line). However, when we apply the model to data outside of the dataset (the blue points), the error becomes much larger. 
This can be generalized to a more universal definition - overfitting happens when your in-sample prediction error is much lower than your out-of-sample prediction error. 

In fact, this is true for not only simple linear regression models, but almost all other methods that attempt to fit a model to describe a certain dataset. Therefore, even at the level of professional statisticians, they are very mindful not to go for the "best fitted" model until they try it out with some new data. 


## What Can We Do?

So what do we do when we don't have new data? In reality, it doesn't seem plausible to always have the "blue points" available to us. One common solution is the idea of "training set" and "test set". 

In practice, statisticians often split up the dataset into a "`training set`" and a "`test set`" as soon as they obtain the raw dataset. The `training set` is where we fit our model around, and the `test set` is where we measure our "out-of-sample error". We keep the `test set` away from us when we fit the model as if we pretend the data in `test set` to be "blue points" (new data). This way, at the end of the analysis, we can use them to check whether our model is overfitting by comparing the training errors and the test errors. The goal is to have the two types of errors comparable. 

Now, when we realize there is overfitting and go back to refit our model, the model might have already "learned" something from the test set, making our test set less reliable in the next round of testing. Statisticians often do what we call "cross-validation" to prevent this problem, but we won't go into it in this blog. In addition, there are many other more advanced strategies that prevent overfitting during the fitting stage, such as early stopping, regularization, and so on. You will learn more about that as you dive deeper into the field of Statistics and Machine Learning! 
