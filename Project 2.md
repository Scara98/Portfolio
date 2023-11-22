## Project Objective
Using data about movies released from 1980 to 2020 I wanted to figure out if there were certain factors that contributed to a movie being successful at the box office. The dataset includes movie title,
movie genre, movie rating, movie score, movie votes, writer, director, star, movie company, movie budget, movie gross, runtime, release date, country released in and country origin.

## Data Source
Dataset was found on the Kaggle website, named "[Movie Industry](https://www.kaggle.com/datasets/danielgrijalvas/movies)" and created by Daniel Grijalvas

## Data tools
* Python
* R Studio
* PowerBI

## Python code

#### Split the Country and date in the released date column

``` python
import pandas as pd

# Read the CSV file into a Pandas 
df = pd.read_csv('movies_project.csv')

# Split the released column into two columns 
df[['released_date', 'released_location']] = df['released'].str.split('(', expand=True)

df['released_location'] = df['released_location'].str.rstrip(')')

# Drop the original released column
df.drop('released', axis=1, inplace=True)

# Write the updated DataFrame to a new CSV file
df.to_csv('my_new_csv_file.csv', index=False, header=True)
```
I separated the country details from the release date, making it easier to use the date column for any needed calculations.

## R Code

#### View the data

``` R

df2 <- read.csv("C:\\Users\\klb81\\OneDrive\\Documents\\Data Analytics Course\\Capstone Project 2\\my_new_csv_file.csv", header = TRUE)

library(dplyr)
library(tidyverse)
```
![Project2_img](https://github.com/Scara98/Portfolio/assets/150705975/c7911f1d-c20c-40b8-90fc-bd270d590473)

#### Clean up the data

```R
# Create a copy of the data frame
df_copy2 <- df2


# Exclude the null values
df_filtered2 <- na.omit(df_copy2)

# Remove year column
df_filtered2 <- df_filtered2[, !(names(df_filtered2) == "year")]
```
![Project2_img2](https://github.com/Scara98/Portfolio/assets/150705975/707689bc-3c5d-4d1a-b32b-d0002d751222)

I did not find the year column to be neccesary any more because each film already had a released date column that had the year included in the date.

#### Add a column for released date month

```R
# Convert the "released_date" column to Date
df_filtered2$released_date <- as.Date(df_filtered2$released_date, format = "%m/%d/%y")

# Create a new column "released_month" with the month names
df_filtered2$released_month <- format(df_filtered2$released_date, format = "%B")
```
![Project2_img3](https://github.com/Scara98/Portfolio/assets/150705975/c743f46f-6016-486b-bb10-1784bea9a8e8)

I created a released month column so I could see if certain times of the year did better in movie profit than other times during the year.

#### Organize the data into an order that is more appeasing

```R
# Rearrange order of columns
new_column_order <- c("name", "rating", "genre", "runtime", "score", "votes", "budget", "gross", "director", "writer", "star", "company","released_date", "released_month", "released_location", "country_origin" )

# Apply changes to data
df_filtered2 <- df_filtered2[, new_column_order]
```
![Project2_img4](https://github.com/Scara98/Portfolio/assets/150705975/5fb70734-6c6f-4bcd-8d2b-1672b3202198)

I reorganized the columns' order just because I found the new order easier to work with for me personally.

#### Run some correlations

```R
runtime <- cor(df_filtered2$gross, df_filtered2$runtime)
## Result 0.2755963

score <- cor(df_filtered2$gross, df_filtered2$score)
## Result 0.2220997

votes <- cor(df_filtered2$gross, df_filtered2$votes)
## Result 0.6148948

budget <- cor(df_filtered2$gross, df_filtered2$budget)
## Result 0.74041
```
![Project2_img5](https://github.com/Scara98/Portfolio/assets/150705975/9b4e0f43-0e3b-4f26-add4-54d64691cd20)

![Pic1](https://github.com/Scara98/Portfolio/assets/150705975/4ec05815-cd4f-41c4-bd87-a5a32b76c61e)

I ran correlations on any column that was numeric so I could see if there were any clear correlations in relation to gross movie income. The *Pearson Correlation Coefficient* between budget and gross was 0.74041. The *Pearson Correlation Coefficient* scale is -1 to 1, with 1 being a total positive correlation. So it is fair to say that budget and gross have a pretty strong positive correlation. 

#### Create multiple tables that compare average gross for different variables

```R
## Create table that shows average gross for rating ##

# Define column to calculate
rating_avg_gross <- df_filtered2 %>% group_by(rating)

# Filter outliers
rating_avg_gross <- rating_avg_gross %>% mutate(count = n())
rating_avg_gross <- rating_avg_gross %>% filter(count > 20)

# Calculate the mean of the gross 
rating_avg_gross <- rating_avg_gross %>% summarise(avg_gross = mean(gross))

# View the results
view (rating_avg_gross)
```
![Project2_img6](https://github.com/Scara98/Portfolio/assets/150705975/1770085f-125e-4e3b-87fe-4d5131798f4d)

```R
## Create table that shows average gross for genre ##

# Define column to calculate
genre_avg_gross <- df_filtered2 %>% group_by(genre)

# Filter outliers
genre_avg_gross <- genre_avg_gross %>% mutate(count = n())
genre_avg_gross <- genre_avg_gross %>% filter(count > 20)

# Calculate the mean of the gross 
genre_avg_gross <- genre_avg_gross %>% summarise(avg_gross = mean(gross))

# View the results
view(genre_avg_gross)
```
![Project2_img7](https://github.com/Scara98/Portfolio/assets/150705975/4eb844f5-29c7-401f-99f4-77dfd5253268)

```R
## Create table that shows average gross for month ##

# Define column to calculate
month_avg_gross <- df_filtered2 %>% group_by(released_month)

# Filter outliers
month_avg_gross <- month_avg_gross %>% mutate(count = n())
month_avg_gross <- month_avg_gross %>% filter(count > 20)

# Calculate the mean of the gross 
month_avg_gross <- month_avg_gross %>% summarise(avg_gross = mean(gross))

# View the results
view(month_avg_gross)
```
![Project2_img8](https://github.com/Scara98/Portfolio/assets/150705975/c85b697f-32d6-4dcc-81a4-1f0fa065b391)

I calculated the average gross of these general factors: month, genre and rating and did not include company, writer, director, and star because more data and research would need to be done
to see if they effect the gross. Maybe some companies, stars, writers, and directors would have high average grossing films in one genre but not another or one time 
period but not today so to focus on general factors that effect a movie's financial sucess I did not include those factors. 

![Pic2](https://github.com/Scara98/Portfolio/assets/150705975/df44265b-69cd-489e-8b5b-62c1ee9711b2)

The top three highest average grossing months:

* May(169M)
* June(167M)
* December(154M)



The bottom three average grossing months:

* January(63M)
* October(60M)
* September(54M)

#### Table to show number of movies released per month by genre

```R
genre_by_month<- table(df_filtered2$released_month, df_filtered2$genre)

view(genre_by_month)
```
![Project2_img9](https://github.com/Scara98/Portfolio/assets/150705975/98a9c812-c1c5-41b0-b2de-c69fbe025922)

#### Table to show month gross sum by genre

```R
genre_sum_by_month <- df_filtered2 %>%
  group_by(genre, released_month) %>%
  summarize(total_gross = sum(gross))

view(genre_sum_by_month)
```
![Project2_img10](https://github.com/Scara98/Portfolio/assets/150705975/31455de3-67b9-4676-8051-469446e11666)

![Pic3](https://github.com/Scara98/Portfolio/assets/150705975/8d4fefb5-f237-4600-b57c-c72c7806751e)

* Action made 65% of the profit and 37% of the movies released.
* Comedy made 13% of the profit and 26% of the movies released.
* Animation made 11% of the profit and 4% of the movies released.
* Adventure made 4% of the profit and 6% of the movies released. 
* Drama made 3% of the profit and 14% of the movies released.
* Horror made 1% of the profit and 4% of the movies released.
* Crime made 1% of the profit and 5% of the movies released.
* Biography made 0.8% of the profit and 3% of the movies released.
* Fantasy made 0.02% of profit and 0.5% of the movies released.

![Pic4](https://github.com/Scara98/Portfolio/assets/150705975/b6991709-36d5-495a-b080-e9fb4c2e365e)

* Action made 47% of the profit and 35% of the movies released.
* Animation made 25% of the profit and 10% of the movies released.
* Comedy made 16% of the profit and 29% of the movies released.
* Drama made 4% of the profit and 11% of the movies released.
* Adventure made 4% of the profit and 4% of the movies released.
* Horror made 1% of the profit and 4% of the movies released.
* Crime made 1% of the profit and 4% of the movies released.
* Biography made 0.5% of the profit and 3% of  the movies released.
* Fantasy made 0.2% of the profit and 0.2% of the movies released.


![Pic5](https://github.com/Scara98/Portfolio/assets/150705975/e743a6dc-c146-4be2-b1e1-c0bc3a20a374)

* Action made 36% of the profit and 21% of the movies released
* Comedy made 18% of the profit and 31% of the  movies released.
* Drama made 14% of the profit and 18% of the movies released.
* Adventure made 13% of the profit and 9% of the movies released.
* Biography made 7% of the profit and 9% of the movies released.
* Animation made 6% of the profit and 4% of the movies released.
* Crime made 4% of the profit and 6% of the movies released.
* Horror made 0.8% of the profit and 3% of the movies released.
* Fantasy made 0.3% of the profit and 0.4% of the movies released.

## Data Conclusions

The data shows clear trends in the film industry. Investing more in a movie budget typically results in higher earnings, highlighting a positive correlation between budget and gross revenue. Timing matters, with May, June, and December being the best months to release a movie and January, October and September are the least desirable months to relase a movie. Action movies consistently make the most money, and both Action and Animation genres have higher average profits per film. Despite high overall profits, Comedies tend to have lower average profits per film. 


