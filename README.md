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

