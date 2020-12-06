
# Coders-HQ Backend

This repository holds the Coders-HQ backend. It is made using [Django](https://www.djangoproject.com/) and [Postgres](https://www.postgresql.org/) as an API backend to the Coders-HQ frontend (based on [React](https://reactjs.org/)) which is hosted on another repository.

## Building

### Pre requisites

1.  python 3
1.  Pip
3.  pipenv
2.  (Optional) docker
2.  (Optional) httpie

### Building locally

1.  run `pipenv shell` in root dir 
1.  run `python manage.py migrate`
1.  run `python manage.py createsuperuser`
1.  Run `python manage.py runserver 0.0.0.0:33325`
1.  On a web browser open localhost:33325

### Building on Docker

1.  make sure you have the correct Database in settings.py
3.  Run `docker-compose up` in root dir and it will create the django and postgres apps, it will also run the web app
1.  On a web browser open localhost:33325

## API

All information related to the API can be found [here](https://documenter.getpostman.com/view/13659675/TVmJjeuV).

## Architecture

The front-end will be located in its own repository which can connect to django's REST framework. The REST framework makes it easy to integrate any frontend to django's API which makes it possible to work on the front and backend separately. The final architecture should look something like this.

```
├──chq_frontend
| ├──public/
| ├──src/
| ├──Dockerfile          
| ├──package.json
| └──package-lock.json
├──chq_backend
| ├──chq_backend/
| ├──media/
| ├──static/
| ├──Dockerfile         
| ├──entrypoint.sh      // bash entrypoint for django to run commands before running the server
| ├──manage.py          
| ├──requirements.txt
| └──settings.ini
└──docker-compose.yaml  //for running multi-conatiner application
```

__Currently the docker-compose.yml is located inside this repository but will eventually be pulled out top integrate the frontend with the backend.__

## Database

Django should be connected to postgres (postgres can be installed locally or using docker) but there is an option to use sqlite for development. __Sqlite should not be used for release.__ To switch between sqlite or postgres use the [migrate function](https://docs.djangoproject.com/en/3.1/topics/db/multi-db/#synchronizing-your-databases) like so:

```
$ ./manage.py migrate   
$ ./manage.py migrate --database=postgres
```

Docker makes it easy to set up postgres. The docker-compose.yaml file creates and connects the two containers (django+postgres) together, you can also create postgres by itself and connect to django which you build locally.

## News

```
news_sites = {
    "codinghorror": "https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fblog.codinghorror.com%2Frss%2F",
    "lambda": "https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Flambda-the-ultimate.org%2Frss.xml",
    "bliki": "https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Fmartinfowler.com%2Fbliki%2Fbliki.atom",
    "joe": "https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Fwww.joelonsoftware.com%2Frss.xml",
    "feed": "https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Ffeeds.feedburner.com%2Ffreetechbooks",
    "orilly": "https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Fradar.oreilly.com%2Findex.rdf",
    "paul": "https://api.rss2json.com/v1/api.json?rss_url=http%3A%2F%2Ffeeds.feedburner.com%2FPaulGrahamUnofficialRssFeed",
    "reddit_programming": "https://www.reddit.com/r/programming/.json"
}
```