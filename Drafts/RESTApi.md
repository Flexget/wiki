---
title: RESTApi
description: 
published: true
date: 2022-09-18T04:58:17.406Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:14.645Z
---

# **REST API **
Anyone interested in developing the webui should feel free to input here.

Will either be a component of webui, or a separately enablable module that webui depends on. Webui can be rewritten as a responsive app that uses this api to interact with FlexGet. All of these endpoints will be under /api or somesuch.

## Design Guidelines
- All data should be transferred as JSON.
- Stick to REST principles as long as it makes sense.
- Should be some easy way for plugins to add their own api endpoints.

## Standard formats
When returning a list of "things" it should be formatted as

```
{
  "items": [list of items]
}
```

When returning an object it should be formatted as 

```
{
  "object": {object}
}
```

# Core Endpoints
## Execution
#### /execution
Executions would be represented with a data structure something like this.

```
{
  "id": <id in queue>,
  "status": "running|pending",
  "current_phase": "input",
  "current_plugin": "rss",
}
```

**GET**
Return a list of running/pending executions.

**POST**
Adds an execution to the queue. Accepts options as JSON (maybe also url parameters).

Returns a stream of the log

### /execution/<id>
**GET**
Get status of execution with given id.

### /execution/<id>/log
**GET** Streams the log for execution with given id.

## Tasks
### /tasks
**GET** list of configured tasks

**POST** Add a new task

### /tasks/<taskname>
**GET** get config for task (other info too? e.g. last run time?)

**DELETE** remove task (what should happen when there are e.g. schedules using it? we probably need events python side scheduler could listen to)

**PUT** update task config

**PATCH** can be used to rename task by sending data `{"name": "thenewname"}`

## Configuration
Not quite sure how this one should go yet. I'm thinking core only provides a way to edit root level config keys (tasks, schedules, etc.) and if we need more granular editing, the plugin would be responsible for the endpoints (e.g. editing individual schedules would be handled by scheduler plugin)

This would likely be redundant, and mostly useful if plugins didn't provide better endpoints themselves

### /config
**GET** List all root elements in config (tasks, schedules, templates, etc.)

**POST** Add config for new root level config section

### /config/<section>
**GET** Get config under root level config section

**DELETE** Remove root level config section

**POST** Replace root level config section

# Plugin Endpoints
## scheduler
### /schedules
**GET** List configured schedules

**POST** Add a schedule

### /schedules/<id>
**GET** Details of schedule (tasks to run, last run, next run)

**PUT** Modify schedule

**DELETE** Remove schedule

## movie_queue
id for movie will be primary key from our database, not online provider id.
Currently movie_queue keeps downloaded movies in its database. Either we'll have to change that, or change this api a bit to have 2 endpoints for pending and grabbed lists. I think I prefer the former.
### /movie_queue
**GET** Return list of movies in the queue

**POST** Add a movie to the queue.
### /movie_queue/<id>
**GET** Return details for movie in queue (not metainfo from imdb etc.)

**DELETE** Remove movie from queue.

**PUT** Change details for movie in queue
## series
## history
### /history
**GET** Get list of items in history
