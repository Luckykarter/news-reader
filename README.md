# News Reader

Web application that holds news in relational database and serves them via web site

The project is publicly available here:

http://34.122.111.115/

### Architecture

Application consists of two parts which are decoupled and connected via API:
- **news-portal** - **Django** based back-end that holds data in relational database and serves it via API
- **news-ui** - **vue.js** based front-end served separately via **nginx** 

### Deployment

The parts of the application are dockerized so are flexible in terms of deployment.

Current implementation uses `docker-compose` for the overall simplicity.

### Source of data

News can be added via several ways:
- Manually in Django admin (including atatching picture)
- From **newsapi.org**
  - via internal Django command
  - via external call to API 

#### Crontab

There is an additional service `crontab` which does periodic scan (once in an hour) of **newsapi.org** for the new articles of the given topics.

New articles are added into database of `news-portal` and shown in `News Reader`

The topics choice is set as comma-separated values of environment variable `NEWS_TOPICS` of service `crontab`. 
