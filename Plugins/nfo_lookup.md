---
title: nfo_lookup
description: 
published: true
date: 2022-09-18T05:08:54.604Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:08:52.026Z
---

# Nfo lookup

Read metadata from an [`nfo` file](http://kodi.wiki/view/NFO_files) when the entries come from the filesystem input. It will also set the
`imdb_id` field of the entry such that if the `imdb_lookup` plugin is also used it will be able to find the correct movie no matter how the movie file is named (or if there are different movies in IMDB with the same name).

**Note**: Currently it only works for movies (the nfo file must have a `<movie>`
tag).

The plugin will do the following:

- Get the name of the file associated with the entry;
- If a file with the same name but a '.nfo' extension exists, read the content of the `nfo` file and add the metadata in the nfo file as 'nfo_something' fields in the entry
- Set the 'imdb_id' field of the entry (if an `<id>` tag with a valid IMDB id is in the `nfo` file.

Config:

```
nfo_lookup: yes
```


Example of a full task
----------------------

Given a folder where each movie is in a subfolder, the task bellow will read all movies and generate an HTML file.

```
filesystem:
  path: SOME_PATH_WITH_MOVIES
  recursive: 2
  regexp: '.*\.(avi|mkv|mp4|m4v|iso)$'
accept_all: yes
nfo_lookup: yes
imdb_lookup: yes
make_html:
  file: ~/tmp/filmes-no-nas.html
```


