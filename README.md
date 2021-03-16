# What is overfitting? 

## Motivation

If you have ever fitted a model, you probably remember that one time you tried again and again just for that last data point to fall on the line. Admit it, we’ve all been there, trying to make our model as "perfect" as possible. However, this is in fact dangerous. It could lead to what is called "overfitting", a phenomenom that is often not encouraged. 

Let’s take a look at sample dataset below. Naturally, an intuitive model would be a curve that runs through the data points like this. <br> 
<img src="https://raw.githubusercontent.com/mmyz88/overfitting-blog/gh-pages/img/points.png" width="250">
<img src="https://raw.githubusercontent.com/mmyz88/overfitting-blog/gh-pages/img/fit1.png" width="270">

However, you might feel a little uncomfortable with that last data point, so you refitted the model with a higher degree to accommodate it. 

<img src="https://raw.githubusercontent.com/mmyz88/overfitting-blog/gh-pages/img/fit2.png" width="270">

Now we have our model tailored to the last data point. But say we want to keep accommodating every single data point, then we might end up with something like this:

<img src="https://raw.githubusercontent.com/mmyz88/overfitting-blog/gh-pages/img/fit3.png" width="270">

It looks like a "perfect" model for our dataset, doesn’t it? Well… consider these new data points, which come from the same population but just weren't included in our initial dataset. How does our model appear to do now? 

<img src="https://raw.githubusercontent.com/mmyz88/overfitting-blog/gh-pages/img/preds.png" width="270">

Not so well is it? We have essentially tailored our model specifically to the existing dataset at hand (yellow points). Our model learned not only the overall trend, but also the detail and noise among the yellow points. Therefore as we collect any new data (blue points), our model would do a bad job because it is tailored to describe the yellow points only, rather than the genuine relationship between the data points. This is the idea of overfitting.


## How Do We Know?

Let’s now formally define `Overfitting`. The key question here is that: *When do we know it overfits?* While it seems to be a subjective question that varies from study to study, we can come up with a generalized way to measure the degree to which a model overfits. That is, to measure the difference between the errors within our dataset and the errors outside of our dataset. 

Let's refer back to our simple example above. When we overfitted, there was little error with our model on the yellow points (remember how all the yeollow points laid on the model line). However, when we apply the model to data outside of the dataset (the blue points), the error becomes much larger. 
This can be generalized to a more universal definition - **overfitting happens when your in-sample prediction error is much lower than your out-of-sample prediction error**. 

In fact, this is true for not only simple linear regression models, but almost all other methods that attempt to fit a model to describe a certain dataset. Therefore, even at the level of professional statisticians, they are very mindful not to go for the "best fitted" model until they try it out with test data. 


## What Can We Do?

In reality, the "blue points" are not always available to us. So what do we do when we don't have new data? One common solution is the idea of "training set" and "test set". 

In practice, statisticians often split up the dataset into a `training set` and a `test set` as soon as they obtain the raw dataset. The `training set` is where we fit our model around, while the `test set` is where we measure our "out-of-sample error". We keep the `test set` away from us when we fit the model, as if we pretend the `test set` are "blue points" (new data). This way, at the end of the analysis, we can use them as new data to check whether our model is overfitting by comparing the training error and the test error. As long as the two errors are comparable, we are good from overfitting. 

Now, when we realize there is overfitting and go back to refit our model, the model might have already "learned" something from the test set, making our test set less reliable in the next round of testing. Statisticians often do what we call "[cross-validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics))" to prevent this problem, but we won't go into detail in this blog. In addition, there are many other more advanced strategies that prevent overfitting during the fitting stage, such as [early stopping](https://en.wikipedia.org/wiki/Early_stopping), [regularization](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a), and so on. You will learn more about that as you dive deeper into the field of Statistics and Machine Learning! 
