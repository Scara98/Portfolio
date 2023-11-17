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


```SQL
-- Replace any null values with identifiable values
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

```SQL
-- Calculate average trip time for different usertypes
SELECT
  usertype,
  AVG(trip_duration) AS average_duration
FROM divvy_trips
GROUP BY
  usertype;
```
![Project1_img3](https://github.com/Scara98/Portfolio/assets/150705975/0cf5e059-3aa9-4916-afdd-d8fd1b8cffb5)
![Pic1](https://github.com/Scara98/Portfolio/assets/150705975/689b22d6-0c44-45c5-b1c9-31073f28583d)
```SQL
-- Count number of subscriber usertypes born each year by gender
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


```SQL
-- Count number of customer usertypes born each year by gender
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
```SQL
-- Count number of each gender in each usertype
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


```SQL
-- Count number of subscriber usertypes that use bikes every day of the week
SELECT
  COUNT(usertype) AS num_users,
  EXTRACT(DOW FROM start_time) AS day_of_week
FROM divvy_trips
WHERE usertype = 'Subscriber'
GROUP BY day_of_week
ORDER BY day_of_week asc;
```
![Project1_img7](https://github.com/Scara98/Portfolio/assets/150705975/3704ff98-44d6-435d-b5a3-6b0a8da95305)

```SQL
-- Count number of customer usertypes that use bikes every day of the week
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

