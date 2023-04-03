---
layout: page
title: Rental bikes membership analysis
description: Google Data Analytics Bike sharing Capstone Project 2023
img: assets/img/Bike.jpg
importance: 1
category: work
---


---

#### Case Study: How Does a Bike-Share Navigate Speedy Success?


**Business task**: We are to design a marketing strategy to convert casual bike
riders to annual members.

The finance analysts determined that it's more profitable for the company to
have membership riders vs casual riders. 

In this study, we need to understand how casual riders differ from membership
riders and how to use that knowledge to influence them to be annual members. 

This is the question we need to answer.

---

> ##### **Case Study Roadmap -Prepare**

The data is located on my laptop. I downloaded it from the given link in the project document from Google.
The data is organized by months. Every month worth of data is in its own 
Excel sheet file. There are a total of 12 Excel sheets for 2022.


###### **Are there issues with bias or credibility in this data?**

Data should adhere to the ROCCC principle:

*R(Reliable)*

The data has the information needed to reach the goal of this study.

It has all the details of the riders that can be analyzed to understand how casual
riders differ from membership riders. Some fields are missing. There lots of blanks in the data. 

We have to determine how to deal with those blanks. We can inject data there or ignore them or delete these rows. 


*O(Original)*

The data is assumed to be original for the purpose of this study. 

*C(Comprehensive)*

The data has all the features that allows us to perform our analysis. However, it has some blanks.

*C(Current)*

The data is current. We are analyzing the last 12 months of data from Jan 2022 to Dec 2022.

*C(Cited)*

The data is cited. It's provided by Motivated International Inc. It's a public data.

###### **How are you addressing licensing, privacy, security, and accessibility?**

*Licensing*

This is a public data. License is available online.

*Privacy*

The data doesn't contain any personally identifiable information.

*security*

The data will be secure on my personal laptop.

*Accessibility*

Data is publicly available but i also have it on my laptop.

###### **How did you verify the data integrity?**


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

###### **How does it help you answer your question?**

By looking at the locations, times, duration of each trip, we can try to see if membership riders have certain preference and we can see how we can provide that to casual members. Still a little unclear to me at this point.

*Are there any problems with the data?*

There are some missing fields. 

---

> #### **Case Study Roadmap -Process**

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

Load the library into the memory space

```{r}
library(tidyverse)
```

Use a read_csv command to import the data into individual data frame.

```{r}

df_jan22<-read_csv("202201-divvy-tripdata.csv") 
df_feb22<-read_csv("202202-divvy-tripdata.csv")
df_mar22<-read_csv("202203-divvy-tripdata.csv") 
df_apr22<-read_csv("202204-divvy-tripdata.csv")
df_may22<-read_csv("202205-divvy-tripdata.csv") 
df_jun22<-read_csv("202206-divvy-tripdata.csv") 
df_jul22<-read_csv("202207-divvy-tripdata.csv") 
df_aug22<-read_csv("202208-divvy-tripdata.csv") 
df_sep22<-read_csv("202209-divvy-publictripdata.csv") 
df_oct22<-read_csv("202210-divvy-tripdata.csv") 
df_nov22<-read_csv("202211-divvy-tripdata.csv") 
df_dec22<-read_csv("202212-divvy-tripdata.csv")

```

At this point, we have 12 different data frames. We need to combine these data frames into one to make it easy for processing. 

Before we do so, we should inspect the column names to make sure that that they are identical across all data frames and that we have the same number of columns. 

Use the command below as an example to print out the columns name of each dataframe to for comparison.

```{r}
colnames(df_jan22)
```

After checking all 12 data frames, all column names are the same.

Next, we need to inspect the column types and make sure they are all of the same type.

Run this command on each dataframe:

```{r}
str(df_jan22)
```

Upon inspecting columns data on each data frame, you can quickly see that  in df_jan22, the started_at and ended_at columns are not in the standard DateTime format (POSIXct format).


<div class="row justify-content-sm-center">
    <div class="col-sm-8">
        {% include figure.html path="assets/img/picture_1_R.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>    

</div>
<div class="caption">
    started_at and ended_at columns are not in the standard DateTime format
</div>





*Note: for more information on this topic, please read this article [link](https://www.neonscience.org/resources/learning-hub/tutorials/dc-convert-date-time-posix-r#:~:text=POSIXct%20method%20converts%20a%20date%2Dtime%20string%20into%20a%20POSIXct%20class.&text=15%3A00%20MDT%22-,as.,often%20your%20local%20time%20zone.)*

Running the 2 lines below, will convert the 2 columns into the needed format.

```{
df_jan22$started_at<-as.POSIXct(df_jan22$started_at,format="%m/%d/%Y %H:%M")
df_jan22$ended_at<-as.POSIXct(df_jan22$ended_at,format="%m/%d/%Y %H:%M")
```

Next, we need to combine the data frames into one. We could use rbind() function or the bind_rows() function from dplyr package. The main difference between the two is that if the number of columns aren't the same between the data frames, rbind() function will throw an error while bind_rows() function will work and will combine the data frames marking the extra column(s) as NA in the respective data frame table. For more information, read this short yet illustrative article : [link](https://www.datasciencemadesimple.com/rbind-in-r/)


Using rbind()

```{r}
cyclistic_df <- rbind ( df_jan22, df_feb22, df_mar22, 
				df_apr22, df_may22, df_jun22, df_jul22,
				df_aug22, df_sep22, df_oct22, df_nov22, df_dec22)
```


Now we need to calculate trip duration for each trip and create a new column called ride_length

```{r}
cyclistic_df_new$ride_length <- difftime(cyclistic_df_new$ended_at, cyclistic_df_new$started_at, units = "mins")
```



Create new columns for further analysis on bike usage during


```{r}
cyclistic_df_new$date <- as.Date(cyclistic_df_new$started_at)
cyclistic_df_new$month <- format(as.Date(cyclistic_df_new$date), "%m")
cyclistic_df_new$day <- format(as.Date(cyclistic_df_new$date), "%d")
cyclistic_df_new$year <- format(as.Date(cyclistic_df_new$date), "%Y")
cyclistic_df_new$day_of_week <- format(as.Date(cyclistic_df_new$date), "%A")
```


Remove rows with NA


```{r}
cyclistic_df_new <- na.omit(cyclistic_df_new)
```

Remove Duplicate rows

```{r}
cyclistic_df_new <- distinct(cyclistic_df_new)
```



Remove rows where ride length is 0 or negative

```{r}
cyclistic_df_new <- cyclistic_df_new[!(cyclistic_df_new$ride_length <=0),]
```

Remove unnecessary columns

```{r}
cyclistic_df_new <- cyclistic_df_new %>%  #remove columns not needed: ride_id, start_station_id, end_station_id, start_lat, start_long, end_lat, end_lng
  select(-c(ride_id, start_station_id, end_station_id,start_lat,start_lng,end_lat,end_lng)) 
```

> #### **Case Study Roadmap -Analyze**


Here are some guiding questions from the capstone project document

###### **How should you organize your data to perform analysis on it?**

The data is organized as a data frame in R. 

We currently have 12 columns and 4,367,646 rows. 

Having the data in R dataframe will make it easy to conduct statistical analysis.

###### **Has your data been properly formatted?**

Yes. Upon running str(cyclistic_df_new), you can see the data format of every column.

Let's conduct descriptive analysis:


*Calculate Total rides*

```{r}
nrow(cyclistic_df_new) : 4367646
```

*calculate total ride duration per customer type*

```{r}
cyclistic_df_new %>%
 group_by(member_casual)%>%
 count(member_casual)
```

*calculate average ride duration per customer type*

```{r}
cyclistic_df_new %>%
 group_by(member_casual)%>%
 summarise(mean_ride_length= mean(ride_length))
```

*Note: casual members use bikes for longer time than members according to the mean*

*calculate mean ride duration per customer type*

```{r}
 cyclistic_df_new %>%
 group_by(member_casual)%>%
 summarise(mean(ride_length))

```

*calculate mode of day of week* 

*we have to create a function to calculate the mode since there is not a built-in function for the mode in R*

For more information about the mode, see this [link](https://www.tutorialspoint.com/r/r_mean_median_mode.htm#)

``` {r}  
getmode <- function(v) {
   uniqv <- unique(v)
   uniqv[which.max(tabulate(match(v, uniqv)))]
}

result <- getmode(cyclistic_df_new$day_of_week)

print(result)

```

*Saturday is the day bikes are used the most*


*If we try to break it down by customer type:*

```{r}
cyclistic_df_new %>%
 group_by(member_casual)%>%
 summarise(getmode(day_of_week))

```

*Saturdays are the days casual riders ride the most and Thursdays are the days member riders ride the most*

*Calculate the average ride_length for users by day_of_week*

```{r}
cyclistic_df_new %>%
 group_by(member_casual, day_of_week)%>%
 summarise(mean(ride_length))

```


*Weekend usage seems to be highest for both type of riders.*

*Ride type aggregation 1*

```{r}
cyclistic_df_new %>%
 group_by(rideable_type, member_casual)%>%
 count(rideable_type)
```


*Ride type aggregation 2*

```{r}
cyclistic_df_new %>%
 group_by(rideable_type)%>%
 count(rideable_type)
```


*So we can see that member bikes never used docked bikes in 2022.* 
*Classic bikes are most widely used followed by electric bikes.*
*Members and casuals seems to prefer classic bikes.*

*Analyze ridership data by type and weekday*

```{r}
cyclistic_df_new %>%
 group_by(member_casual, day_of_week)%>%
 summarise(number_of_rides = n(),average_duration = mean(ride_length)) %>%
 arrange(member_casual,day_of_week )
```

> #### **Case Study Roadmap -Share**

Here are some guiding questions from the capstone project document

###### **Were you able to answer the question of how annual members and casual riders use Cyclistic bikes differently?**

Yes, we should that both types of memberships use the bikes differently.

###### **What story does your data tell?**

The data we saw so far tells that riders differ in their behaviour based on the membership types and that it's possible to create a campaign to 
influence casual riders to become members.

Members and casual riders show different usage patterns in how they use the bikes. From the findings above we took note of the following:

* Members take more rides throughout the week vs casual users
* Saturdays are the days casual riders ride the most and Thursdays are the days member riders ride the most
* Casual riders take less trips/rides but for longer durations of time vs members
* Casual members use bikes for longer time than members according to the mean duration value
* Member bikes never used docked bikes in 2022
* Members and casuals seems to prefer classic bikes
* Classic bikes are most widely used followed by electric bikes


###### **How do your findings relate to your original question?**

The original question was about how to influence the casual rider to become a member. Looking at the analaysis above, we were able
to draw some conclusions about the usage behaviour of both types of riders and therefore we can come up with recommendations on how to achieve the goal of this study.

###### **Who is your audience? What is the best way to communicate with them?**

Lily Moreno and Cyclistic are internal and external audience. The best way to communicate the findings is to draft a presentation that summrizes
the study with visualizations.

###### **Can data visualization help you share your findings?**

Yes.

###### **Is your presentation accessible to your audience?**

Yes.




*Let's visualize the number of rides by rider type*

*Convert day_of_week from charachter to Ordered Factor so we can sort it. Otherwise it will sort alphapatically*

```{r}
cyclistic_df_new$day_of_week <- wday(cyclistic_df_new$started_at, label = TRUE)

cyclistic_df_new %>% 
 group_by(member_casual, day_of_week)%>%
 summarise(number_of_rides = n(),average_duration = mean(ride_length)) %>%
 arrange(member_casual,day_of_week) %>%
 ggplot(aes(x=day_of_week, y = number_of_rides, fill = member_casual))+
 geom_col(position = "dodge")

```

<div class="row justify-content-sm-center">
    <div class="col-sm-8">
        {% include figure.html path="assets/img/picture_2_R.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>    

</div>
<div class="caption">
    Plot the Day of Week vs the Number of rides by rider type
</div>

*Members take more rides throughout the week vs casual users*

*Let's create a visualization for average duration*

```{r}
cyclistic_df_new %>% 
 group_by(member_casual, day_of_week)%>%
 summarise(number_of_rides = n(),average_duration = mean(ride_length)) %>%
 arrange(member_casual,day_of_week) %>%
 ggplot(aes(x=day_of_week, y = average_duration, fill = member_casual))+
 geom_col(position = "dodge")

```
<div class="row justify-content-sm-center">
    <div class="col-sm-8">
        {% include figure.html path="assets/img/picture_3_R.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>    

</div>
<div class="caption">
    Plot the Day of Week vs Average Duration by rider type
</div>


*Casual riders take less trips/rides but for longer durations of time vs members*

Here are the 2 Visualizatoins above using interactive Tablue Public Dashboard


<div class="row justify-content-sm-center">
    <div class="col-sm-12">

        <p align="center"><iframe src="https://public.tableau.com/views/Capstoneproject_16794594078290/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link:showVizHome=no&:embed=true"
        width="750" height="600"></iframe></p>
    </div>    

</div>
<div class="caption">
    Tablue Public Dashboard
</div>






*EXPORT SUMMARY FILE FOR FURTHER ANALYSIS*

```{r}
counts <- aggregate(cyclistic_df_new$ride_length ~ cyclistic_df_new$member_casual + cyclistic_df_new$day_of_week, FUN = mean)
write.csv(counts, file = 'avg_ride_length.csv')
```



> #### **Case Study Roadmap -Act**

Here are some guiding questions from the capstone project document

###### **What is your final conclusion based on your analysis?**

In order to get more casual riders to buy a membership my top recommendations are:

* Give discounts/promotions for longer rides when you have a membership.
* Give discounts/promotions on Saturdays when you have a membership.
* Longer rides can get some type of rewards program when they become members.

###### **How could your team and business apply your insights?**

Send a mass email to all casuals with the promotions to sign up.


###### **Suggested next steps**

* Redo the project using pandas library in Python.
* Redo using Bigquery SQL.
* Create move Viz using Tablue.

###### **Resources**

* Kaggle RODRIGO LEYVA Google Data Analytics (Cyclistic) Capstone Project [link](https://www.kaggle.com/code/rodrigoleyva2/google-data-analytics-cyclistic-capstone-project#STEP-4:-CONDUCT-DESCRIPTIVE-ANALYSIS)
* Kelly J Adams Google Data Analytics (Cyclistic) Capstone Project [link](https://www.kellyjadams.com/post/google-capstone-project)
* ITAMAR Cyclistic Case Study [link](https://www.kaggle.com/code/itamargn/cyclistic-case-study/report)