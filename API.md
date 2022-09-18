---
title: API
description: 
published: true
date: 2022-09-18T04:52:33.289Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:48:23.548Z
---

# API

Flexget offers a JSON API, that is the basis of its [Web-UI](/Web-UI) and can also be used independently of it. 

### Enabling the API
To enable the API add the following to your config.yml:
```yaml
web_server: yes
```
That will enable the API and Web-UI on 0.0.0.0 with the port 5050 by default. 
You can also set a different port using:
```yaml
web_server: 8080
```
The API can also run without running the Web-UI:
```yaml
web_server:
  bind: 0.0.0.0
  port: 8080
  web_ui: no
```
Then run Flexget in daemon mode:
```text
flexget daemon start
```

### Using the API
The API uses SwaggerUI documentation which can be accessed via the configured host and IP. For example: `http://localhost:5050/api/`.  

### Authentication
Set a password and start flexget in daemon mode to start the web server.

```text
flexget web passwd <some_password>
```

The login username is `flexget` and the password is what you set above. 

You can also use an authorization header to access the API with the following format:
```text
Authorization: Token <TOKEN>
```

You can view the API token using the following CLI commands

View existing token: `flexget web showtoken`  
Regenerate token: `flexget web gentoken`

To use the API, the user must be authenticated via a site cookie or attach the Token to each request.  

To authenticate via cookies you need to submit a POST request to the `/auth/login/` endpoint as such:
```HTTP
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" -d "{
  \"password\": \"password\",
  \"username\": \"username\"
}" "http://localhost:5050/api/auth/login/?remember=true"
```
### API Versions
The API version is returned via the `API-Version` header in all request.  
At this time there is only 1 API version provided, but that is subject to change it the future

### ETags
All of the API `GET` methods provide `etag` headers for cache control. 

### Pagination
Some endpoints provide server side pagination. Those endpoints are:
- `/series/`
- `/series/<ID>/episodes/`
- `/series/<ID>/episodes/<ID>/releases/`
- `/entry_list/<ID>/entries/`
- `/movie_list/<ID>/movies/`
- `/failed/`
- `/seen/`
- `/history/`
- `/rejected/`
- `/plugins/`

These endpoint implement [RFC5988](https://tools.ietf.org/html/rfc5988) via `Link` header, in a similar manner to [GitHub](https://developer.github.com/guides/traversing-with-pagination/) as such:
```text
Link: <http://127.0.0.1:5050/api/movie_list/1/movies/?per_page=5&order=desc&sort_by=title&page=1>; rel="prev",
<http://127.0.0.1:5050/api/movie_list/1/movies/?per_page=5&order=desc&sort_by=title&page=3>; rel="next",
<http://127.0.0.1:5050/api/movie_list/1/movies/?per_page=5&order=desc&sort_by=title&page=7>; rel="last"
```
The following request paramateres are used for pagination requests:
- `per_page`: Maximum number of results to be returned per response. Default is 50, limited to 100.
- `page`: Page number. Default is `.  

Some endpoints support sorting. The following parameters are then relevant:
- `sort_by`: Attribute name to sort by. See different endpoint documenation for options and defaults.
- `order`: Can be `desc` or `asc`. Default is `desc`.

The `rel` relation can be `next`, `prev` or `last` for each of the links, stating their relation the the returned object. There is no `first` relation since that is always `page=1`.

In addition, the response contains the following headers:
- `Total-Count`: Total number of entities
- `Count`: Actual number of entities returned in current page

## Additional notes:

- Some endpoint operation operate on you config file. Those that do will CHANGE IT LAYOUT AND STRCUTURE AND REMOVE ALL REMARKS. Do not operate via the API if those things are of value to you (functionality will remain intact).