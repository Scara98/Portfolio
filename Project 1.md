## Project objective
This capstone project was given to me by the Google Data Analytics course on Coursera. The made up company they made for the scenario
is called Cyclistic which is a bike-share company based in Chicago. Cyclistic's director of marketing wants to determine how Casual Riders 
and Annual Members differ in their use of Cyclist bikes. Casual riders pay per ride for the citibike or per day whereas Annual members pay a fixed amount every year.
The director then wants to use the discovered information to create marketing strategies that will help convert Casual riders to Annual members.

## Project Data Source
[Google Data Analytics course](https://www.coursera.org/professional-certificates/google-data-analytics) on Coursera provided: The divvy trip 2018 Quarter 2 dataset


## PostgreSQL Code
#### Make a table to import data into
```SQL
                       create table divvy_trips (trip_id numeric,
						 start_time timestamp,
						 end_time timestamp,
						 bike_id numeric,
						 trip_duration numeric,
						 from_station_id numeric,
						 from_station_name text,
						 to_station_id numeric,
						 to_station_name text,
						 usertype text,
						 gender text,
						 birthyear numeric);
```
![Project1_img](https://github.com/Scara98/Portfolio/assets/150705975/458fa299-b793-4777-9e91-da34e5812d4f)

#### Replace any null values with identifiable values
```SQL
UPDATE divvy_trips
SET trip_id = COALESCE(trip_id, '0'),
       start_time = COALESCE(start_time, '0001-01-01 00:00:00'),
       end_time = COALESCE(end_time, '0001-01-01 00:00:00'),
       bike_id = COALESCE(bike_id, '0'),
       trip_duration = COALESCE(trip_duration, '0'),
       from_station_id = COALESCE(from_station_id, '0'),
       from_station_name = COALESCE(from_station_name, 'N/A'),
       to_station_id = COALESCE(to_station_id, '0'),
       to_station_name = COALESCE(to_station_name, 'N/A'),
       usertype = COALESCE(usertype, 'N/A'),
       gender = COALESCE(gender, 'N/A'),
       birthyear = COALESCE(birthyear, '0');
```
![Project1_img2](https://github.com/Scara98/Portfolio/assets/150705975/00dc75c8-1501-4773-b2ad-7d80b732cb84)

#### Calculate average trip time for different usertypes
```SQL
SELECT
  usertype,
  AVG(trip_duration) AS average_duration
FROM divvy_trips
GROUP BY
  usertype;
```
![Project1_img3](https://github.com/Scara98/Portfolio/assets/150705975/0cf5e059-3aa9-4916-afdd-d8fd1b8cffb5)


![Pic1](https://github.com/Scara98/Portfolio/assets/150705975/981214df-25c6-4bb7-ab6f-eb25647dffd0)

*Annual Subscribers'* average trip time is 14 minutes whereas *Casual Riders'* average trip time is 64 minutes.

#### Count number of subscriber usertypes born each year by gender
```SQL
SELECT
  birthyear,
  gender,
  usertype,
  COUNT(*) AS count_of_people
FROM divvy_trips
WHERE usertype = 'Subscriber'
GROUP BY birthyear, gender, usertype
ORDER BY count_of_people desc;
```
![Project1_img4](https://github.com/Scara98/Portfolio/assets/150705975/d4e3ed50-cf48-47a9-8ab9-a7351e469442)

#### Count number of customer usertypes born each year by gender

```SQL
SELECT
  birthyear,
  gender,
  usertype,
  COUNT(*) AS count_of_people
FROM divvy_trips
WHERE usertype = 'Customer'
GROUP BY birthyear, gender, usertype
ORDER BY count_of_people desc;
```
![Project1_img5](https://github.com/Scara98/Portfolio/assets/150705975/1a3cc7d7-ac74-4d25-8d4e-92bdee65ec7f)


![Pic2](https://github.com/Scara98/Portfolio/assets/150705975/c2931a57-abcb-490f-8e7d-d77cb1c55516)

**44%** of Annual Subscribers are ages 25-35
**43%** of Casual Riders are ages 25-35

#### Count number of each gender in each usertype

```SQL
SELECT
  usertype,
  gender,
  COUNT(*) AS total_count,
  COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (PARTITION BY usertype) AS percentage
FROM divvy_trips
GROUP BY usertype, gender
ORDER BY usertype, gender;
```
![Project1_img6](https://github.com/Scara98/Portfolio/assets/150705975/c270db5d-f901-4f10-8700-010e62f9c639)

![Pic3](https://github.com/Scara98/Portfolio/assets/150705975/e8a8794f-3bd8-48d5-9be7-486fbb07656d)

Males make up **75%** of Annual Subscribers and **61%** of all cyclists.

#### Count number of subscriber usertypes that use bikes every day of the week

```SQL
SELECT
  COUNT(usertype) AS num_users,
  EXTRACT(DOW FROM start_time) AS day_of_week
FROM divvy_trips
WHERE usertype = 'Subscriber'
GROUP BY day_of_week
ORDER BY day_of_week asc;
```
![Project1_img7](https://github.com/Scara98/Portfolio/assets/150705975/3704ff98-44d6-435d-b5a3-6b0a8da95305)

#### Count number of customer usertypes that use bikes every day of the week

```SQL
SELECT
  COUNT(usertype) AS num_users,
  EXTRACT(DOW FROM start_time) AS day_of_week
FROM divvy_trips
WHERE usertype = 'Customer'
GROUP BY day_of_week
ORDER BY day_of_week asc;
```
![Project1_img8](https://github.com/Scara98/Portfolio/assets/150705975/ff23175b-d66d-423f-8819-aeebaa159c8e)


![Pic4](https://github.com/Scara98/Portfolio/assets/150705975/d5c22d4f-c682-488d-89a3-45833d34fa36)

Annual Subscribers made up **85%** of weekday rides.
Annual Subscribers only made up **61%** of the rides during the weekend.

## Project Conclusions
* Males between ages 25-35 are the majority rider type for Annual Subscribers
* Casual Riders mostly use bikes on weekends whereas Annual Subscribers mostly use them during the weekdays
* Annual Subscribers use bikes for short periods of time whereas Casual Riders use bikes for long periods of time

## Recommendations
* Target audience should be males 25-35
* Create annual subscription that is cheaper but only allows use on weekends
* Put advertisements on social media used by targeted demographic 

