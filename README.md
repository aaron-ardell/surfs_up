# Surfs Up
## Overview

Analyzing the weather data for the Oahu area for the client, they've requested temperature data specifically for the months of June and December. They are looking to determine if their surf and ice cream shop business would be sustainable year-round. 

We'll utilize the sqlite database provided with the data from 9 weather stations in the Oahu area. After inserting our dependencies, our first order of business will be generating a query that will pull the temperature data by month. Then we'll generate a DataFrame from the list we'd created. Finally, we'll repeat the process for the other month so we have two databases for June and December independently.  

## Results

We'll start off with the temperature summary statistics for months of June.

![This is an image](https://github.com/aaron-ardell/surfs_up/blob/main/june_describe.png)

Next, we'll look at the December information.

![This is an image](https://github.com/aaron-ardell/surfs_up/blob/main/dec_describe.png)

Key differences between these two datasets are minimal, which is promising for the client's desire to make his business year-round.

* The average temperatures during the months of June and December are within 4 degrees fahrenheit of each other.
* The max temperature is within 2 degrees of each other.
* Only the lowest temperature has a more signifigant fluctuation, 8 degrees lower in December than in June.

In fact, we can look at histograms of June and December to compare the most frequent temperature readings.

First, June...

![This is an image](https://github.com/aaron-ardell/surfs_up/blob/main/june_temp_hist.png)

And then, December...

![This is an image](https://github.com/aaron-ardell/surfs_up/blob/main/dec_temp_hist.png)

## Summary

In summary, the temperature data reinforces the idea that the client's shop could be a year-round operation in the Oahu location.

There's more data that can be pulled from the dataset to aid our client in determining the viability of his potential enterprise.

We can easily pull the percipitation for the months of June and December with a similar strategy.

```
j_date_str = "06"
june_temp = session.query(Measurement.date, Measurement.prcp).\
  filter(func.strftime("%m", Measurement.date) == j_date_str).all()
june_temp_df = pd.DataFrame(june_temp)
june_temp_df.describe()

d_date_str =  "12"
dec_temp = session.query(Measurement.date, Measurement.prcp).\
    filter(func.strftime("%m", Measurement.date) == d_date_str).all()
dec_temp_df = pd.DataFrame(dec_temp)
dec_temp_df.describe()
```

![This is an image](https://github.com/aaron-ardell/surfs_up/blob/main/june_prcp.png) ![This is an image](https://github.com/aaron-ardell/surfs_up/blob/main/dec_prcp.png)

Just as with the temperatures, we can see that percipitation datasets for the month of June and December only have minor variances and nothing that would produce enough impact to deter the client from his desire to make it a year-round business.



