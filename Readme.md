
![system schema](Images/title_banner.png)

![R](https://img.shields.io/badge/r-%23276DC3.svg?style=for-the-badge&logo=r&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white) ![Google](https://img.shields.io/badge/google-4285F4?style=for-the-badge&logo=google&logoColor=white) ![Coursera](https://img.shields.io/badge/Coursera-%230056D2.svg?style=for-the-badge&logo=Coursera&logoColor=white)

![Repository Size](https://img.shields.io/github/repo-size/HectorMelendez/Google_DA_Capstone_2022) ![License](https://img.shields.io/github/license/HectorMelendez/Google_DA_Capstone_2022) ![Lines of Codes](https://img.shields.io/tokei/lines/github.com/HectorMelendez/Google_DA_Capstone_2022) ![Last Commit](https://img.shields.io/github/last-commit/HectorMelendez/Google_DA_Capstone_2022)

### Student: Hector Melendez
Data Analyst | Producer & Audio Engineer

- 🖥 Website: https://hectormelendez.github.com
- 💼 LinkedIn: https://www.linkedin.com/in/melendezriverahector
- 🗃 Github: https://github.com/HectorMelendez
- 📧 Email: melendezriverahector@gmail.com
- 🎧 Hasy Miller (Me 🥲): https://open.spotify.com/artist/6dALey2jKCMx4JdxN2ycVj
---

# **Table of Contents**
1. [Analysis Overview](#analysis_overview)
2. [Data License and Privacy](#license_privacy)
3. [Initial Dataset Information](#initial_dataset)
4. [Importing Required Packages](#importing_packages)
   1. [Step 1: Data Collecting](#step_1)
   2. [Step 2: Combining Data](#step_2)
   3. [Step 3: Cleaning Data](#step_3)
   4. [Step 4: Descriptive Analysis](#step_4)
   5. [Step 5: Data Visualization](#step_5)
   6. [Step 6: Export Summary](#step_6)


---
## **Analysis Overview** <a name="about_the_task"></a>

**<span style="color: green;">The Goal: </span>**
Design marketing strategies aimed at converting casual riders into annual members.

I’m a junior data analyst working with the marketing team for Cyclistic (fictional company), a bike-share company in Chicago.

In 2016, Cyclistic launched a successful bike-share ordering. Since then, the program has grown to a fleet of 5,824 bicycles that are geo-tracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

---
### ⚠️ _Data License and Privacy_ <a name="license_privacy"></a>

>Cyclistic it’s a fictional business name.  All the datasets used on this capstone project were provided by Google & Coursera with respective licenses.

>The data has been made available by Motivate International Inc. under this [license]. This is public data that you can use to explore how different customer types are using Cyclistic bikes. But note that data-privacy issues prohibit you from using riders’ personally identifiable information. This means that you won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

## **Initial Dataset Information** <a name="initial_dataset"></a>

Dataset provided by Google & Coursera under the Motivate International Inc. [license].

  |      |       |
  | ---- | ----- |
  | **Original Data Source:** |   https://divvy-tripdata.s3.amazonaws.com/index.html |
  | **Dataset Date Range:** | September 2021 - July 2022 (12 months) |
  | **Dataset Reliable:**   | Yes, the data is [reliable]. |
  | **Dataset Cleaned:**   | No. Dataset clean up it’s required. |
  | **Data Versioning:**  | It will be available here on [GitHub].  |

---
![system schema](Images/lets_begin.png)

## **Importing Required Packages** <a name="importing_packages"></a>

Programming language used: [R-Language](https://www.r-project.org/)

R-Packages used to prepare, clean, manipulate and visualize data:

```r
library(tidyverse)    # For data import and wrangling
library(lubridate)    # Helps wrangle date attributes
library(ggplot2)      # Helps visualize data
getwd()               # Displays your working directory

#Sets your working directory to simplify calls to data:
setwd("/Users/HasyDevelopment/Desktop/Divvy_Exercise/csv")
```

> ⚠️ Important: Make sure to use your own project directory instead of mine.

---
## Step 1: Data Collecting <a name="step_1"></a>

Let's load the _.csv_ files into RStudio:

```r
q1_2020 <- read_csv("Cyclistic_Trips_2020_Q1.csv")
q2_2019 <- read_csv("Cyclistic_Trips_2019_Q2.csv")
q3_2019 <- read_csv("Cyclistic_Trips_2019_Q3.csv")
q4_2019 <- read_csv("Cyclistic_Trips_2019_Q4.csv")
```

The dataset provided by Cyclistic covers a full year of real user inputs.  Make sure to use correct naming conventions on the files and a very organize folder structure.

---
## Step 2: Combining Data <a name="step_2"></a>

We start comparing the column names each of the files to verify consistency.
While the names don't have to be in the same order, they **DO NEED TO MATCH** perfectly before we can use a command to join them into one file.

```r
# Rename and replace the column names of the data frame
colnames(q4_2019)
colnames(q3_2019)
colnames(q2_2019)
colnames(q1_2020)  # Going-forward table design

# Rename columns to make them consistent with q1_2020
(q4_2019 <- rename(q4_2019
                   ,ride_id = trip_id
                   ,rideable_type = bikeid
                   ,started_at = start_time
                   ,ended_at = end_time
                   ,start_station_name = from_station_name
                   ,start_station_id = from_station_id
                   ,end_station_name = to_station_name
                   ,end_station_id = to_station_id
                   ,member_casual = usertype))

(q3_2019 <- rename(q3_2019
                   ,ride_id = trip_id
                   ,rideable_type = bikeid
                   ,started_at = start_time
                   ,ended_at = end_time
                   ,start_station_name = from_station_name
                   ,start_station_id = from_station_id
                   ,end_station_name = to_station_name
                   ,end_station_id = to_station_id
                   ,member_casual = usertype))

(q2_2019 <- rename(q2_2019
                   ,ride_id = "01 - Rental Details Rental ID"
                   ,rideable_type = "01 - Rental Details Bike ID"
                   ,started_at = "01 - Rental Details Local Start Time"
                   ,ended_at = "01 - Rental Details Local End Time"
                   ,start_station_name = "03 - Rental Start Station Name"
                   ,start_station_id = "03 - Rental Start Station ID"
                   ,end_station_name = "02 - Rental End Station Name"
                   ,end_station_id = "02 - Rental End Station ID"
                   ,member_casual = "User Type"))
```

Now let's covert the data to text (string). That way we can combine the data easily and without any problems.  **Remember to visually inspect the dataset and look for incongruences**:

```r
# Convert all data to text (string)
str(q1_2020)
str(q4_2019)
str(q3_2019)
str(q2_2019)

# Convert ride_id and rideable_type to character so that they can stack correctly
q4_2019 <-  mutate(q4_2019, ride_id = as.character(ride_id)
                   ,rideable_type = as.character(rideable_type))

q3_2019 <-  mutate(q3_2019, ride_id = as.character(ride_id)
                   ,rideable_type = as.character(rideable_type))

q2_2019 <-  mutate(q2_2019, ride_id = as.character(ride_id)
                   ,rideable_type = as.character(rideable_type))
```

Nicely done.  Now we stack the individual quarter's into a **one big data frame**:

```r
# Stack individual quarter's
all_trips <- bind_rows(q2_2019, q3_2019, q4_2019, q1_2020)
```

---
## Step 3: Cleaning Data <a name="step_3"></a>

We start by removing: _lat, long, birthyear, and gender_ fields as this data was dropped at the beginning of 2020.

```r
# (-c) is to select all except the mentioned columns:
all_trips <- all_trips %>%
  select(-c(start_lat, start_lng, end_lat, end_lng, birthyear, gender, "01 - Rental Details Duration In Seconds Uncapped", "05 - Member Details Member Birthday Year", "Member Gender", "tripduration"))
```

Let's inspect the tables that has been created. Take your time, and make sure that everything looks correct :)

```r
colnames(all_trips)     # List of column names.
nrow(all_trips)         # How many rows are in data frame?
dim(all_trips)          # Dimensions of the data frame?
head(all_trips)         # Show first 6 rows of data frame. Also tail(qs_raw).
str(all_trips)          # See list of columns and data types.
summary(all_trips)      # Statistical summary of data. Mainly for numerics.
```

> **⚠️ IMPORTANT:** We have a few problems we need to fix ASAP.

- (1) In the "_member_casual_" column, there are two names for members ("_member_" and "_Subscriber_") and two names for casual riders ("_Customer_" and "_casual_"). We will need to consolidate that from four to two labels.

- (2) The data can only be aggregated at the ride-level, which is too granular. We will want to add some additional columns of data -- such as day, month, year -- that provide additional opportunities to aggregate the data.

- (3) We will want to add a calculated field for length of ride since the 2020Q1 data did not have the "_tripduration_" column. We will add "_ride_length_" to the entire dataframe for consistency.

- (4) There are some rides where _"tripduration"_ shows up as negative, including several hundred rides where Cyclistic took bikes out of circulation for Quality Control reasons. We will want to delete these rides.

In the "_member_casual_" column, replace "_Subscriber_" with "_member_" and "_Customer_" with "_casual_". Before 2020, Cyclistic used different labels for these two types of riders ... we will want to make our dataframe consistent with their current nomenclature.

> "_Level_" is a special property of a column that is retained even if a subset does not contain any values from a specific level. Begin by seeing how many observations fall under each _usertype_.

```r
#Pulling values from the list object that the function returns ($ operator)
# See this answer: https://stackoverflow.com/questions/31327303/use-of-and-operators-in-r
table(all_trips$member_casual)

# Reassign to the desired values (we will go with the current 2020 labels)
all_trips <-  all_trips %>%
  mutate(member_casual = recode(member_casual
                           ,"Subscriber" = "member"
                           ,"Customer" = "casual"))

# Check to make sure the proper number of observations were reassigned
table(all_trips$member_casual)
```

Add columns that list the date, month, day, and year of each ride. This will allow us to aggregate ride data for each month, day, or year ... before completing these operations we could only aggregate at the ride level.
> More on date formats in R found at this link: https://www.statmethods.net/input/dates.html

```r
#The default date format is: yyyy-mm-dd
all_trips$date <- as.Date(all_trips$started_at)
all_trips$month <- format(as.Date(all_trips$date), "%m")
all_trips$day <- format(as.Date(all_trips$date), "%d")
all_trips$year <- format(as.Date(all_trips$date), "%Y")
all_trips$day_of_week <- format(as.Date(all_trips$date), "%A")
```
Now we add "_ride_length_" calculation to _all_trips_ (in seconds).  Then inspect the structure of the columns (take  your time) before we convert _ride_length_ from Factor to numeric so we can run calculations on:

```r
# Check this reference code:
# https://stat.ethz.ch/R-manual/R-devel/library/base/html/difftime.html
all_trips$ride_length <- difftime(all_trips$ended_at,all_trips$started_at)

# Inspect the structure of the columns
str(all_trips)

# Convert "ride_length" from Factor to numeric
is.factor(all_trips$ride_length)
all_trips$ride_length <- as.numeric(as.character(all_trips$ride_length))
is.numeric(all_trips$ride_length)
```

Finally let's remove the "bad" data. The dataframe includes a few hundred entries when bikes were taken out of docks and checked for quality by Cyclistic or _ride_length_ was negative. We will create a new version of the dataframe (v2) since data is being removed:

```r
# See this reference code:
# https://www.datasciencemadesimple.com/delete-or-drop-rows-in-r-with-conditions-2/
all_trips_v2 <- all_trips[!(all_trips$start_station_name == "HQ QR" | all_trips$ride_length<0),]
```

## Step 4: Descriptive Analysis <a name="step_4"></a>

My favorite part of being a data analyst: _making sense of data_. Let's  start with the **descriptive analysis** on _ride_length_ (all figures in seconds):

```r
mean(all_trips_v2$ride_length)    # Straight average (ride_length / rides)
median(all_trips_v2$ride_length)  # Midpoint number in the ASC (ride_length)
max(all_trips_v2$ride_length)     # Longest ride
min(all_trips_v2$ride_length)     # Shortest ride

# Condense everything to one line using summary() on the specific attribute
summary(all_trips_v2$ride_length)
```

Let's compare Cyclistic Members and Casual Users:

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = mean)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = median)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = max)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual, FUN = min)
```

Now we retrieve the **average ride time** by each day for members vs casual users:

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)
```

> Notice that the days of the week are out of order. Let's fix that:

```r
all_trips_v2$day_of_week <- ordered(all_trips_v2$day_of_week, levels=c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))
```
Now, let's run again the **average ride time** by each day for members vs casual users:

```r
aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)
```

Lastly, we analyze ridership data by type and weekday:

```r
all_trips_v2 %>%
  mutate(weekday = wday(started_at, label = TRUE)) %>%  #creates weekday field using wday()
  group_by(member_casual, weekday) %>%          #groups by usertype and weekday
  summarise(number_of_rides = n()							  #calculates the number of rides and average duration
  ,average_duration = mean(ride_length)) %>% 		# calculates the average duration
  arrange(member_casual, weekday)								# sorts
```

---
## Step 5: Data Visualization <a name="step_5"></a>

Now we prepare the fun stuff.  Data visualization will help non-technical people to understand your data.  No body likes complicated data... except data analysts 🥲

```r
# Let's visualize the number of rides by rider type
all_trips_v2 %>%
  mutate(weekday = wday(started_at, label = TRUE)) %>%
  group_by(member_casual, weekday) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%
  arrange(member_casual, weekday)  %>%
  ggplot(aes(x = weekday, y = number_of_rides, fill = member_casual)) +
  geom_col(position = "dodge")

# Let's create a visualization for average duration
all_trips_v2 %>%
  mutate(weekday = wday(started_at, label = TRUE)) %>%
  group_by(member_casual, weekday) %>%
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>%
  arrange(member_casual, weekday)  %>%
  ggplot(aes(x = weekday, y = average_duration, fill = member_casual)) +
  geom_col(position = "dodge")
```

---
## Step 6: Export Summary <a name="step_6"></a>

Our very final line of code. Create a .csv file that we will visualize in Excel, Tableau, or a presentation software:

```r
counts <- aggregate(all_trips_v2$ride_length ~ all_trips_v2$member_casual + all_trips_v2$day_of_week, FUN = mean)
write.csv(counts, file = '~/Desktop/avg_ride_length.csv')
```
> **⚠️ IMPORTANT:** This file location is for a Mac. If you are working on a PC, change the file location accordingly (most likely "C:\Users\YOUR_USERNAME\Desktop\...") to export the data. You can read more here: https://datatofish.com/export-dataframe-to-csv-in-r/



[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [license]: <https://www.divvybikes.com/data-license-agreement>
   [GitHub]: <https://github.com/HectorMelendez>
   [reliable]: <>
