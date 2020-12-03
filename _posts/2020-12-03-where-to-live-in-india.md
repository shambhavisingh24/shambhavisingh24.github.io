---
title: "WHERE TO LIVE IN INDIA: BASED ON YOUR CLIMATE PREFERENCE"
date: 2020-12-03T15:34:30-04:00
categories:
  - projects
tags:
  - R

---

I recently started using R and while surfing through the internet I landed on [Maëlle Salmon’s](https://masalmon.eu/2017/11/16/wheretoliveus/) blog which started a trend on twitter to find the ideal cities to live in different parts of world, based on your climate preference. I thought why not do something like this for India. Maëlle Salmon’s blog post was originally inspired by [xkcd comic](https://xkcd.com/1916/).
So, let’s find where you should live in India!

-------
**DATASET**

To get the weather data for cities in India, I used Maëlle Salmon’s library package **“riem”**.The riem package allows you to access the weather data from all over the world collected at airport weather stations.
My main reasons for using this package was:
1. It is very convenient!
2. To get actual data from Indian Meteorology department, you have to fill a request form, and then they will send you the data.

I didn’t know what the code was to access weather data of Indian airports, hence I used **riem_networks** command to do it.

```data <- riem_networks
library(dplyr)
data %>% filter(name == "India ASOS")
```
Running this we find that code for India is **“IN__ASOS”**. To see the different airports in India we use **riem_stations** command. Using the command, we see that there are 96 airports in the Indian network, I am sure that India has more airports but for the sake of this project we will only consider these. Also, from the id column we see that airports are coded in the ICAOstandard rather than the IATA standard.

I, personally, did not know there are two types of codes for airport, and the one that I and most probably you use while booking tickets is IATA(New Delhi as DEL, Mumbai as BOM).

To get the city data with ICAO standard, I used this [page](https://airportcodes.io/en/all-airports/?filters[country]=IN), wherein I simply copied ICAO, name, and municipality column and pasted it in an excel sheet. I then loaded this sheet into R using **read_csv** function from **readr** library.

Now that we have city data, we want to acquire weather data. We use the riem package for this. We use the same code from Maëlle Salmon’s original blogpost where she uses **map_df()**, from **purrr** library, to apply **riem_measures()** on each airport code with the output being a lovely data frame!
I checked this Wikipedia page, to see how summer and winter are defined by the India Meteorological Department. Basically, this is how they define the seasons
-**Winter**, occurring from December to February
-**Summer** lasts from March to May

```library(purrr)
summer_weather <- map_df(indian_airports$ICAO, riem_measures, date_start = "2019-03-01", date_end = "2019-05-31")
View(summer_weather)
winter_weather <- map_df(indian_airports$ICAO, riem_measures, date_start = "2018-12-01", date_end = "2019-02-28")
View(winter_weather)
```
The result is two gigantic datasets of around 175,180 observations each along with 31 variables ranging from dew point temperature, wind direction in degrees from north, relative humidity, and many more!
Please load the riem package before using riem_measure. Also, while getting the winter data don’t forget to put previous year in date_start, or else you will get error!

-----


