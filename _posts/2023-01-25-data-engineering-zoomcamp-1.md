---
layout: post
title:  "Data Engineering Zoomcamp Week 1"
date:   2023-01-24 11:23:29 -0500
categories: data-engineering
---

I recently found and started the free [Data Engineering Zoomcamp offered by DataTalks.Club](https://github.com/DataTalksClub/data-engineering-zoomcamp). I'm enjoying the content so far, in particular how it builds up concepts step by step, for instance:
    - playing around with a jupyter notebook to take a look at the data and put it into the db
    - turning the jupyter notebook into a script
    - dockerizing the script and running it locally
    - running the docker container remotely

The lecture videos are about a year old now, so some of the specifics of the instructions are slightly off from what they were at the time of publishing. This was not a big deal, a bit of drift in documentation is inevitable, but I could see how this might cause some problems for people with less experience in setting up their environments. Hopefully these hiccups didn't dissuade any from continuing with the program!

One more notable change was that the [TLC Trip Record Data website](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) now provides its data in the  `.parquet` format. Apache Parquet is a column oriented data storage format with built-in compression. I've never worked with it before but I'm glad to know it exists. I followed the tutorial using the parquet data
    - Pandas does have a `read_parquet` function, but it required installing `pyarrow` as a dependency to work
    - the parquet file specified the format of each column, so it wasn't necessary to do a datetime conversion on the datetime columns
    - the `read_parquet` doesn't have a chunksize parameter like `read_csv` does so I had to implement my own iterator 

When I got to the homework questions, I realized that the more up to date `.parquet` data had slightly more records than old `.csv` from a year ago, so there was a chance that my homework results may not exactly match. This is not an unusual issue with datasets, I used to see issues with data going "stale" all the time at my last job. So in the end I ended up going back and ingesting the data from the backed up `.csv` files for the homework.

I'm looking forwards to the rest of the course, especially looking at the tools available through GCP. 
