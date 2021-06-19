---
title: 'Web Scraping Service'
date: '20210616141508'
category: 'project'
tags: ['idea', 'project', 'scraping']
---

# web scraping service
Jordan and I had a project idea for automated web scraping that would be a competitor
to the [ScraperBox](https://scraperbox.com) using a Docker container system.

## Services
We would just need to serve API keys to the client then:
* Have them send requests to us with the URL to scrape
* More premium users can persist data on our end?
* Return the HTML
* Maybe have a generalized "sanitation" for known types?
    * Try to parse to JSON as best as we can (cleanly)
    * User defined JSON parsing fields in the request?
* Avoids captchas using modern techniques? (Premium)
* Does JavaScript using Selenium (Premium)
* Offer request concurrency for more money (Premium)
* Proxies? (Premium)

## Structure
Docker
Django
Celery -> Autoscaling worker containers
PostgreSQL -> RDS
