# News Reader

Web application that holds news in relational database (the implementation uses PostgreSQL) and serves them via website

The project is publicly available here:

http://34.122.111.115/

### Architecture

Application consists of two parts which are decoupled and connected via API:
- **news-portal** - **Django** based back-end that holds data in relational database and serves it via API
- **news-ui** - **vue.js** based front-end that retrieves and shows news. Served separately via **nginx**.

### Deployment

The parts of the application are dockerized so are flexible in terms of deployment.

Each part has its own repository and included as submodules of this (parent) repository that is responsible for bringing up the application.

Current implementation uses `docker-compose` for the overall simplicity.

`docker-compose.override.yml` is used for running the project locally - it exposes frontend on port `81` and backend - on port `8000`. 
Thus, to bring up application in production - `docker-compose` file should be explicitly set:

```
docker-compose -f docker-compose.yml up --build -d
```

### Source of data

News can be added via several ways:
- Manually in Django admin (including attaching picture)
- From **newsapi.org**
  - via internal Django command
  - via external call to API 

#### Crontab

There is an additional service `crontab` which does periodic scan (once in an hour) of **newsapi.org** for the new articles of the given topics.

New articles are added into database of `news-portal` and shown in `News Reader`

The topics choice is set as comma-separated values of environment variable `NEWS_TOPICS` of service `crontab`. 
