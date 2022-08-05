# Google Data Analytics Certication ---capstone_project

# Data-driven Analysis for a Bike-share Company: An Insight into Cyclistic’s bike-share dataset to maximize marketing strategy

# Introduction
Launched in 2016, Cyclistic, a successful bike-share company runs a bike-share program in Chicago, USA. They also offer reclining bikes, hand tricycles, and cargo bikes, to make bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. Currently, the program has grown to a fleet of 5,824 bicycles, geotracked and locked into a network of 692 docking stations across Chicago, where the bikes can be unlocked from one station and returned to any other station in the system anytime. Majority of the riders opt for traditional bikes; about 8% of riders use the assistive options, about 30% of the riders use the bike to commute to work every day, while the rest more likely use it for leisure. With the flexibility in the pricing plans packages namely: single-ride passes, full-day passes, and annual memberships, the users are divided into two (2) major categories: the casual riders (customers who purchase single-ride or full-day passes) and the cyclistic members (those who purchase annual memberships).
Reports of the business finance analysts revealed that, though the flexibility in the pricing packages attracts more customers, the company generates more profits from the cyclistic members (those who purchase annual memberships). The director of marketing also believes that the key to the business future growth is to maximize the cyclistic members’ population. Therefore, the need to identify how these two (2) users groups differ in the use of the services Cyclistic bike-share company offer as well as design marketing strategies to ensure conversion of casual riders into annual members for optimum business opportunities.

# Case Study Roadmap
The Stepwise guidelines used in this project aligns with the “Data Analysis Process” roadmap taught in the Data Analytics Certification Programme by Google. The guidelines include six (6) different phases which are:  Ask, Prepare, Process, Analyse, Share and Act.  

# The “Ask” Phase 
Business Task:
-------------------------------------------------------------------------------------------------------------
The objective of this project is to (1) provide data-driven insights into how casual riders and annual members differ in the usage of Cylistic share-bikes. 	
(2) Identify trends and patterns of users using the company’s historical data to design marketing strategies needed to convert casual riders into annual members

Key Stakeholders: 
-------------------------------------------------------------------------------------------------------------
•	The director of marketing: She is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels. 
•	Marketing Analytics Team: A team of data analysts at Cyclistic who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy. I joined this team of data analysts six months ago as a Junior Data Analyst.
•	Executive Teams: The notoriously detailed-oriented executives at Cyclistic that will decide whether to (dis) approve the recommended marketing program.

# The “Prepare” Phase
These public, open datasets were made available under this license. This thus addresses licencing, privacy, security, and accessibility concerns.  It was thereafter downloaded as zip files, extracted as a spreadsheet in a csv file format and subsequently stored in a folder. I ensured the datasets were free of issue regarding bias or credibility during the data preparatory process by implementing ROCCC methodology. (ROCCC signifies Reliable, Original, Comprehensive, Current and Cited).

# The ”Process” Phase
Here, the data was prepped for its readiness for analysis. R programming Language was employed at this stage. R programming Language is regarded as a good tool useful for data cleaning, organising and of course analysis. It is known for its ability to handle large datasets, superb analysis, and visualisation prowess, it is easily accessible, data-centric and open-source with an active user community. 

Steps: 
-------------------------------------------------------------------------------------------------------------
1: Data Sourcing and Preparation

The data sets were resident in the Cylistic's company database as a zipped CSV files. It was downloaded as 2021 data containing 12 zipped files for each month. Data was then extracted into folders after with RStudio was used to carry out data preparation, cleaning and exploration. 

The first step was to set up the environment in the RStudio by loading the required packages

```{r loading packages}
library(tidyverse)
library(tidyr)
library(readr)
library(ggplot2)
library(lubridate)
library(skimr)
library(stringr)
```
2: Data Importation and Appending
The different CSV files were imported into the RStudio using the read_csv() package

```{r cyclistic_share_bike datasets}
jan <-read_csv("DAC8_case_study/202101-divvy-tripdata.csv")
feb <-read_csv("DAC8_case_study/202102-divvy-tripdata.csv")
mar <-read_csv("DAC8_case_study/202103-divvy-tripdata.csv")
apr <-read_csv("DAC8_case_study/202104-divvy-tripdata.csv")
may <-read_csv("DAC8_case_study/202105-divvy-tripdata.csv")
jun <-read_csv("DAC8_case_study/202106-divvy-tripdata.csv")
july <-read_csv("DAC8_case_study/202107-divvy-tripdata.csv")
aug <-read_csv("DAC8_case_study/202108-divvy-tripdata.csv")
sept <-read_csv("DAC8_case_study/202109-divvy-tripdata.csv")
oct <-read_csv("DAC8_case_study/202110-divvy-tripdata.csv")
nov <-read_csv("DAC8_case_study/202111-divvy-tripdata.csv")
dec <-read_csv("DAC8_case_study/202112-divvy-tripdata.csv")
```
They were thereafter appended into a single dataframe for easier cleaning and have a better understanding the data structure using glimpse(), str() and colnames() functions

```{r binding dataset into a dataframe}
ride_data <- bind_rows(jan, feb, mar, apr, may, jun, july, aug, sept, oct, nov, dec)
```
Rows: 5,595,063
Columns: 13

$ ride_id            <chr> "E19E6F1B8D4C42ED", "DC88F20C2C55F27F", "EC45C94683FE3F27", "4FA453A75AE3…

$ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", "electric_bike", "elec…

$ started_at         <dttm> 2021-01-23 16:14:19, 2021-01-27 18:43:08, 2021-01-21 22:35:54, 2021-01-0…

$ ended_at           <dttm> 2021-01-23 16:24:44, 2021-01-27 18:47:12, 2021-01-21 22:37:14, 2021-01-0…

$ start_station_name <chr> "California Ave & Cortez St", "California Ave & Cortez St", "California A…

$ start_station_id   <chr> "17660", "17660", "17660", "17660", "17660", "17660", "17660", "17660", "…

$ end_station_name   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, "Wood St & Augusta Blvd", "California…

$ end_station_id     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, "657", "13258", "657", "657", "657", …

$ start_lat          <dbl> 41.90034, 41.90033, 41.90031, 41.90040, 41.90033, 41.90041, 41.90039, 41.…

$ start_lng          <dbl> -87.69674, -87.69671, -87.69664, -87.69666, -87.69670, -87.69676, -87.696…

$ end_lat            <dbl> 41.89000, 41.90000, 41.90000, 41.92000, 41.90000, 41.94000, 41.90000, 41.…

$ end_lng            <dbl> -87.72000, -87.69000, -87.70000, -87.69000, -87.70000, -87.71000, -87.710…

$ member_casual      <chr> "member", "member", "member", "member", "casual", "casual", "member", "me…

The dataset contains 5,595,063 rows distributed in 13 columns representing variables about the bike-share users.

2: Data Cleaning (removing duplicates, nulls and renaming conventions)
```{r remove duplicates}
ride_data_new <- distinct(ride_data)
```
```{r remove null values and rename variables}
ride_data_new <- drop_na(ride_data)
ride_data_new <- ride_data_new %>% 
  rename(bike_type = rideable_type, user_type = member_casual)
```
3: Data Transformation for further cleaning
Creation of new columns which are the trip_duration (this represent the length of each ride), week and month each ride occured
```{r calculate trip duration}
ride_data_cleaned <- mutate(ride_data_new, trip_duration = as.numeric(ended_at - started_at)/60)
```
```{r Calculate week and month trip occured}
ride_data_cleaned <- mutate(ride_data_cleaned, 
   trip_day = format(as.Date(ride_data_new$started_at), "%A"), 
   trip_month = format(as.Date(ride_data_cleaned$started_at), "%B"))
```
4: Overview of the cleaned dataset
```{r data preview}
glimpse(ride_data_cleaned)
```
Rows: 4,588,302

Columns: 16

$ ride_id            <chr> "B9F73448DFBE0D45", "457C7F4B5D3DA135", "57C750326F9FDABE", "4D518C65E33…

$ bike_type          <chr> "classic_bike", "electric_bike", "electric_bike", "electric_bike", "clas…

$ started_at         <dttm> 2021-01-24 19:15:38, 2021-01-23 12:57:38, 2021-01-09 15:28:04, 2021-01-…

$ ended_at           <dttm> 2021-01-24 19:22:51, 2021-01-23 13:02:10, 2021-01-09 15:37:51, 2021-01-…

$ start_station_name <chr> "California Ave & Cortez St", "California Ave & Cortez St", "California …

$ start_station_id   <chr> "17660", "17660", "17660", "17660", "17660", "17660", "17660", "17660", …


$ end_station_name   <chr> "Wood St & Augusta Blvd", "California Ave & North Ave", "Wood St & Augus…

$ end_station_id     <chr> "657", "13258", "657", "657", "657", "KA1504000135", "KA1504000113", "KA…

$ start_lat          <dbl> 41.90036, 41.90041, 41.90037, 41.90038, 41.90036, 41.90037, 41.90036, 41…

$ start_lng          <dbl> -87.69670, -87.69673, -87.69669, -87.69672, -87.69670, -87.69679, -87.69…

$ end_lat            <dbl> 41.89918, 41.91044, 41.89918, 41.89915, 41.89918, 41.90327, 41.89047, 41…

$ end_lng            <dbl> -87.67220, -87.69689, -87.67218, -87.67218, -87.67220, -87.63446, -87.70…

$ user_type          <chr> "member", "member", "casual", "casual", "casual", "member", "member", "m…

$ trip_duration      <dbl> 7.216667, 4.533333, 9.783333, 8.950000, 10.150000, 20.550000, 6.000000, …

$ trip_day           <chr> "Sunday", "Saturday", "Saturday", "Saturday", "Sunday", "Friday", "Tuesd…

$ trip_month         <chr> "January", "January", "January", "January", "January", "January", "Janua…

# The "Analyse" Phase
A dive into the cyclistic bike share data for insights

1: Insight into Average ride length of users
```{r calculate ave_ride_lenght Vs. Users_type }
avg_trip_duration <- ride_data_cleaned %>%
  group_by(user_type) %>%
  summarise(avg_trip_duration = mean(trip_duration))
```
```{r ave_ride_length Vs. User_type}
ggplot(avg_trip_duration)+
  geom_col(mapping=aes(x = user_type, y = avg_trip_duration, fill = user_type))+
  labs(title = "Average Trip Duration Vs. User_type", subtitle = "Cyclistic Customer")
```
![Average Trip Duration Vs  User_type](https://user-images.githubusercontent.com/106023180/183000770-726385bb-8a51-4083-a538-e1b9d6545f5d.png)

Across the year 2021, the casual bike users spent more time using the bike-share facilities than the users with membership subscription
  
 2:Average trip length by users on days of the week
 
 ```{r avg_ride_length by users Vs.days_of_week}
avg_trip_week <- ride_data_cleaned %>%
  group_by (trip_day, user_type) %>%
  summarise(number_of_trips = n(), average_trip_length = mean(trip_duration),
            .groups = 'drop') %>%
arrange(user_type, trip_day)
```
```{r visualisation of average_ride_length of users Vs. days_of_week}
ggplot(avg_trip_week)+
  geom_col(mapping = aes(x = trip_day, y = average_trip_length, fill = user_type))+
  labs(title = "Average Weekly Trip Vs. User_type", subtitle = "Cyclistic Customer")
```
![Average Weekly Trip Vs  User_type](https://user-images.githubusercontent.com/106023180/183001747-74d73cfc-d2a9-45fd-8179-b491453cfe4c.png)

Across the days of week, it shows that the casual users spent more time using the bikes at the weekends than the week days. This indicates that most of the casual riders use the bikes for leisures and exercises.
  
3: Number of trips by users on weekly basis
```{r count_of_rides by users Vs. days_of_the_week}
avg_trip_week <- ride_data_cleaned %>%
  group_by(trip_day, user_type) %>%
  summarise(number_of_trips = n(), average_trip_length = mean(trip_duration),
            .groups = 'drop') %>%
  arrange(user_type, trip_day)
```
```{r visualise count_of_rides by users Vs. days_of_the_week}
ggplot(avg_trip_week)+
  geom_col(mapping = aes(x = trip_day, y = number_of_trips, fill = user_type))+
  labs(title = "Number of Weekly Trip Vs. User_type", subtitle = "Cyclistic Customer") 
```
![Number of Weekly Trip Vs  User_type](https://user-images.githubusercontent.com/106023180/183002726-23ddb0c4-7450-45b1-b8b0-0d077f18956a.png)

Here, there were higher numbers of the membership subscribers using the bikes during the weekdays as compared to the casual users. This could be as a result that most members use the facilities as a mode of transportation to commute to work and few spends time biking at weekends

4: Number of trips by users on monthly basis

```{r avg_ride_length by users Vs.month_of_year}

avg_trip_month <- ride_data_cleaned %>%
  group_by(trip_month, user_type) %>%
  summarise(number_of_trips = n(), average_trip_length = mean(trip_duration),
            .groups = 'drop') %>%
  arrange(user_type, trip_month) 
```
```{r visualisation of month_of_year by users Vs. average_ride_length}
ggplot(avg_trip_month)+
  geom_col(mapping = aes(x = trip_month, y = number_of_trips, fill = user_type))+
  labs(title = "Number of Monthly Trip Vs. User_type", subtitle = "Cyclistic Customer")
```
![Number of Monthly Trips Vs  User_type](https://user-images.githubusercontent.com/106023180/183003286-08838a64-d79e-422c-9615-48081f41ccf8.png)

Seasons of the year:

a) Winter: December, January, February


b) Spring: March, April, May

Summer: June, July, August

Autumn: September, October, November

Over the months of the year, both categories of users ride more during the summer season and the first month of autumn compared to other seasons of the year

#

