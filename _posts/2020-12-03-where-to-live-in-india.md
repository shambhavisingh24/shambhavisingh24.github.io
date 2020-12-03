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

