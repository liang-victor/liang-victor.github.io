---
layout: post
title:  "Data Engineering Zoomcamp Week 2 Prefect"
date:   2023-02-06 00:01:29 -0500
categories: data-engineering
---

The second module of the [Data Engineering Zoomcamp](https://github.com/DataTalksClub/data-engineering-zoomcamp) covered workflow orchestration using Prefect.

For years I've used bash/python scripts with cronjobs, and in the last year airflow, for orchestrating and executing these types of workflows. It's always good to see what others use for these types of situtations.

My first impression was that setting it up was very streamlined. The first flow was basically just a plain python script, except with some `@flow` and `@task` decorators above the function definitions. The first session did have a lot of "magic" behind the scenes, but I was glad to learn that there were some useful things that could be configured behind the scenes:

    - everything seems to work via the REST API, you can communicate with it either via python modules or CLI
    - you can either run your own server (Orion) or use a hosted solution from Prefect (Prefect Cloud). I'm not entirely certain whether Orion is just meant for local development purposes or if people deploy their own version in production too.
    - Running a python script with decorated functions will give observability to the execution details, and also gain automatic retries, notifications, etc. What's nice is that it still feels like you're running regular python, you can pass data from one task to another via function arguments as usual. 
    - Starting up a worker will pick up flows from a queue to execute

Overall I think the development experience is much nicer than on airflow, as even just running airflow via docker-compose on my laptop was a huge resource drain. Also as mentioned before it's nice to be able to pass variables along without having to use Xcom.