---
layout: post
title:  "Data Engineering Zoomcamp Week 3 BigQuery"
date:   2023-02-13 00:03:29 -0500
categories: data-engineering
---

This week used BigQuery. 

I remember a couple of years ago, a few customers were just a bit over the line of "too much data" for us to be able to load the data as a single pandas dataframe. I ended up modifying our reporting pipeline for those customers to partition the data into monthly partitions, and splitting up report elements that queried data in only the previous month vs those that were reporting on longer range trends that needed more. For those trends, I would load up iteratively load up one month at a time, compute the aggregates I was interested and save them, then move on to the next file. This added some more overhead to the process but it enabled us to generate these reports without running out of memory. 

BigQuery allows us to do stuff like this while maintaining a clean SQL interface. It can even be set up by simply pointing it to a bucket on GCS or S3. I really wish that I knew about this tool back then! It can also set up a bunch of ML modeling as well.