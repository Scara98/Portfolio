## Python code
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

## R Code
``` R

df2 <- read.csv("C:\\Users\\klb81\\OneDrive\\Documents\\Data Analytics Course\\Capstone Project 2\\my_new_csv_file.csv", header = TRUE)

library(dplyr)
library(tidyverse)
```
![Project2_img](https://github.com/Scara98/Portfolio/assets/150705975/c7911f1d-c20c-40b8-90fc-bd270d590473)

```R
# Create a copy of the data frame
df_copy2 <- df2


# Exclude the null values
df_filtered2 <- na.omit(df_copy2)

# Remove year column
df_filtered2 <- df_filtered2[, !(names(df_filtered2) == "year")]
```
![Project2_img2](https://github.com/Scara98/Portfolio/assets/150705975/707689bc-3c5d-4d1a-b32b-d0002d751222)

```R
# Convert the "released_date" column to Date
df_filtered2$released_date <- as.Date(df_filtered2$released_date, format = "%m/%d/%y")

# Create a new column "released_month" with the month names
df_filtered2$released_month <- format(df_filtered2$released_date, format = "%B")
```
![Project2_img3](https://github.com/Scara98/Portfolio/assets/150705975/c743f46f-6016-486b-bb10-1784bea9a8e8)

```R
# Rearrange order of columns
new_column_order <- c("name", "rating", "genre", "runtime", "score", "votes", "budget", "gross", "director", "writer", "star", "company","released_date", "released_month", "released_location", "country_origin" )

# Apply changes to data
df_filtered2 <- df_filtered2[, new_column_order]
```
![Project2_img4](https://github.com/Scara98/Portfolio/assets/150705975/5fb70734-6c6f-4bcd-8d2b-1672b3202198)

```R
# Run correlations
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

```R
# Table to show number of movies released per month by genre
genre_by_month<- table(df_filtered2$released_month, df_filtered2$genre)

view(genre_by_month)
```
![Project2_img9](https://github.com/Scara98/Portfolio/assets/150705975/98a9c812-c1c5-41b0-b2de-c69fbe025922)

```R
# Table to show month gross sum by genre
genre_sum_by_month <- df_filtered2 %>%
  group_by(genre, released_month) %>%
  summarize(total_gross = sum(gross))

view(genre_sum_by_month)
```
![Project2_img10](https://github.com/Scara98/Portfolio/assets/150705975/31455de3-67b9-4676-8051-469446e11666)
