# Window Functions Lab

## Introduction

In this lab, we'll try to answer questions with the given dataset. [Description](https://ride.capitalbikeshare.com/system-data) to the dataset is here. We'll be using Capital Bikeshare trip dataset. 

## Objectives
- Understand how & when to use window functions

1. First, open up the attached csv file in the data folder. Examine the data, and create a table called `bikeshare` using SQL DDL.


```python
# Your solution
```

Once the table is created, follow below step to import csv file into the sqlite database.

```
sqlite> .mode csv
sqlite>.import <absolute_path_to_csv_file> bikeshare
```
If you're unsure of the absolute path of the csv file, navigate to the directory from your terminal/shell, then type `pwd`. It should yield something like this:
```
(learn-env) ➜  Downloads pwd
/Users/myUserName/Downloads
(learn-env) ➜  Downloads 
```
Once the csv file is imported, execute the following command to see if you're able to fetch the data.
```
SELECT * FROM bikeshare LIMIT 10;
```

2. We're interested in the average bike ride from a specific starting station. We also want to order by the start time. How can we achieve this using window function?


```python
# Your solution
```


```python
# __SOLUTION__
SELECT start_station, duration, AVG(duration) OVER
(PARTITION BY start_station ORDER BY start_time DESC) AS average_duration
FROM bikeshare;
```

3. How can we see how many rides were taken from each starting station?


```python
# Your solution
```


```python
# __SOLUTION__
SELECT start_station, COUNT(*) OVER (PARTITION BY start_station) AS cnt
FROM bikeshare;
```

4. How can we get which starting station was most popular? Could we get top 10?


```python
# Your solution
```


```python
# __SOLUTION__
SELECT start_station RANK() OVER (PARTITION BY start_station) AS rank
FROM bikeshare LIMIT 10;
```

Try the above question with `DENSE_RANK()` to see if you get different answers!
