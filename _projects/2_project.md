---
layout: page
title: Boston Housing Market
description: Boston Housing Market ML deployment Project 2023
img: assets/img/boston.jpg
importance: 2
category: work
---


---

#### Case Study: How to create a Machine Learning model and deploy it to production using Dockers, Postman, Github Actions and Heroku?

This is a project walk thru from Krish Naik:[Github](https://github.com/krishnaik06/bostonhousepricing)

You can access the entire code on my repository: [My Project repo](https://github.com/mokasha2020/bostonhousepricing)

The dataset is for Boston house-price data based on a paper that was done by Harrison, D. and Rubinfeld, D.L. that was published in 1978.

The dataset was available on older sklearn dataset versions. It has been deprecated in v 1.0 and was removed in v 1.2.

In order to get the data, you can download it from the CMU.edu website directly as shown below.

```

data_url = "http://lib.stat.cmu.edu/datasets/boston"
raw_df = pd.read_csv(data_url, sep="\s+", skiprows=22, header=None)
data = np.hstack([raw_df.values[::2, :], raw_df.values[1::2, :2]])
target = raw_df.values[1::2, 2]

```

### Summary of the steps taken to create the code:

1- Create the Linear regression model as shown in Linear Regression ML Implementation.ipynb. Go thru the code and the comments to understand the dataset, 
 prepare it, do basic analysis, train the model, do performance matrix and prediction of new data. 
2- Export the model to a pickle file. See regmodel.pkl
3- Create a new environment in VS code.
4- Create a FLASK web app and a simple webpage to take user input to predict the data.
5- Create a Procfile for Heroku deployment.
6- Create a Docker file to containrise the app.

Further suggested steps to be implemented:

* Change the sklearn model used. Instead of Linear Regression, try Neural network using Tensor flow.
* Create a chat bot to take user data for prediction and spit out the result instead of the html page we created.
* Use a different dataset.





