---
layout: page
title: Rental bikes membership analysis
description: Google Data Analytics Bike sharing Capstone Project 2023
img: assets/img/Bike.jpg
importance: 1
category: work
---

This is a WORK IN PROGRESS- NOT COMPLETE- TEST

# Case Study: How Does a Bike-Share Navigate Speedy Success?


Business task:We are to design a marketing strategy to convert casual bike
riders to annual members.

The finance analysts determined that it's more profitable for the company to
have membership riders vs casual riders. 

In this study, we need to understand how casual riders differ from membership
riders and how to use that knowledge to influence them to be annual members. 

This is the question we need to answer.

Case Study Roadmap -Prepare

The data is located on my laptop. I downloaded it from the given link in the project document from Google.
The data is organized by months. Every month worth of data is in its own 
Excel sheet file. There are a total of 12 Excel sheets for 2022.


Are there issues with bias or credibility in this data?

Data should adhere to the ROCCC principle:

R(Reliable)

The data has the information needed to reach the goal of this study.

It has all the details of the riders that can be analyzed to understand how casual
riders differ from membership riders. Some fields are missing. There lots of blanks in the data. 

We have to determine how to deal with those blanks. We can inject data there or ignore them or delete these rows. 


O(Original)

The data is assumed to be original for the purpose of this study. 

C(Comprehensive)

The data has all the features that allows us to perform our analysis. However, it has some blanks.

C(Current)

The data is current. We are analyzing the last 12 months of data from Jan 2022 to Dec 2022.

C(Cited)

The data is cited. It's provided by Motivated International Inc. It's a public data.

How are you addressing licensing, privacy, security, and accessibility?

Licensing

This is a public data. License is available online.

Privacy

The data doesn't contain any personally identifiable information.

security

The data will be secure on my personal laptop.

Accessibility

Data is publicly available but i also have it on my laptop.

How did you verify the data integrity?






This data is assumed to be the whole population of riders in every month. It's not a sample.

Therefore, I don't think we have any issues with bias or data credibility.

There are 4 different types of bias that could happen when we collect a sample of data:

1- Sample Bias: This is not an issue here since we are assuming we have data for the whole population. 

Also, we aren't asking people to answer any surveys. There is no risk of timing bias for example.

The data covers 12 months worth of rides. We are not collecting data thru certain time of the year.

2- Observer Bias: This is not an issue here since we are not making observations. This data was taken from 

the database based on the details of every ride.

3- Interpretation Bias: This is not an issue for the raw data. We will see how it is when we analyze the data.

4- Confirmation Bias: This is not issue for raw data. 


How does it help you answer your question?

By looking at the locations, times, duration of each trip, we can try to see if membership riders have certain preference and we can see how we can provide that to casual members. Still a little unclear to me at this point.

Are there any problems with the data?

There are some missing fields. 


Case Study Roadmap -Process

In this step, first thing I tried was to use Excel to clean the data. 

While using Excel to clean, filter, add columns to the data was easy in one Excel sheet, 

repeating the task with the remaining 11 sheets would be a waste of time. I could have combined

all 12 sheets into one using a manual or automated process. However, the result would be a huge excel sheet

that could have over 1 million row which may make processing the sheet very slow. I decided to use

R to clean up the data. After all, R is a very powerful and useful tool that allows us to process huge 
amount of data. 

After deciding to use R, I went to my Posit(RStudio account on the cloud) in order to use it for this project. However, I was faced with the limited RAM memory in my free account when I started importing
the csv files into the work space using the read_csv command.

So I decided not to mess to much with Rstudio on the cloud and just use Rstudio that I installed on my laptop. Now I have all the memory in my laptop available for this project :)

Now, let's dig into the code:

Install the tidyverse package that will be used to clean and process the data.

```{r}
install.packages('tidyverse')
```






#To give your project a background in the portfolio page, just add the img tag to the front matter like so:

#    ---
#    layout: page
#    title: project
#    description: a project with a background image
#    img: /assets/img/12.jpg
#    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}