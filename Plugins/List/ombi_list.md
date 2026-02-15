---
title: Ombi list
description: 
published: true
date: 2026-02-15T00:35:12.399Z
tags: 
editor: markdown
dateCreated: 2026-02-15T00:35:12.399Z
---

# Ombi List Plugin — Quick Guide

The `ombi_list` plugin integrates FlexGet with your Ombi instance, allowing you to list, add, match, or remove movie and TV requests using the Ombi API.

## Options

| Option        | Type   | Required | Description                                                                          |
|---------------|--------|----------|--------------------------------------------------------------------------------------|
| `url`         | str    | Yes      | Ombi server URL (e.g. `https://ombi.yourdomain.com`)                                 |
| `api_key`     | str    | Yes      | Ombi API key                                                                         |
| `type`        | str    | Yes      | List type: `movies`, `shows`, `seasons`, or `episodes`                               |
| `status`      | str    | No       | Filter by request status (`requested`, `approved`, `denied`) (movies/episodes only)  |
| `hide_available` | bool | No      | Exclude available episodes (episodes only, default: `no`)                            |
| `on_remove`   | str    | No       | Use `"deleted"` to actually delete when used in `list_remove`                        |

*For `shows` and `seasons`, `status` and `hide_available` are not supported.*

## Example

```yaml
tasks:
  list_denied_movies:
    ombi_list:
      url: https://ombi.server.com
      api_key: yourapikey
      type: movies
      status: denied
    accept_all: yes
    exec: echo "{{title}} (Status: {{ombi_status}})"
```

## Notes

- Use with `list_add`, `list_remove`, `list_match`, or directly in a task.
- Use the correct `type` for your items (`movies`, `shows`, `seasons`, `episodes`).
- Only `movies` and `episodes` support `status` and `hide_available`.

```