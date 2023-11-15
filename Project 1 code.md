```SQL
-- Make a table to import data into
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

```SQL
-- Calculate average trip time for different usertypes
SELECT
  usertype,
  AVG(trip_duration) AS average_duration
FROM divvy_trips
GROUP BY
  usertype;
```

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

