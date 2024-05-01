# News-Reader backend

Django based back-end for the news reader project.

The project is intended to dockerized deployment and has no coupling with any front-end.

## Features

The application holds news data (articles) in relational database (PostgreSQL) and serves it via REST API.

### Entering the data

There are several ways of inputting data into the app

There is an integration with resource **newsapi.org** to get the articles. 

**NOTE** that to be able to retrieve data from newapi.org - 
the environment variable `NEWS_PORTAL_KEY` has to be set with the relevant API key.  

#### Via command 
```
python manage.py get_articles_from_newsapi --query="topic1, topic2" --period=25
```
`query` holds comma-separated values for topic to search
`period` holds period of time in the past to get the news

This command can be scheduled as a job to update news in background.

#### Via API
There is a separate API endpoint which triggers downloading the news of the given topic from the given period.

See Swagger UI for more details.

### Getting the data
The data can be retrieved via REST API. It's implemented with Django Rest Framework.

Pagination, filtering and sorting are supported.

The endpoints can be found in Swagger UI


### Testing the app
The app is unit tested with `pytest` and has target coverage of 100%

To execute tests run:
```
pytest --cov news
```

### Build the app
The app contains `Dockerfile` and can be built via 
```
docker build .
```
More info about deployment info can be found in the parent repository 

**NOTE** That application can't be built/started "as-is" because it requires secret environment variable `SECRET_KEY` which is not included in this repo.

