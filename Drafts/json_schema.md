---
title: json_schema
description: 
published: true
date: 2022-09-18T04:58:51.912Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:49.178Z
---

Ideas for how to incorporate json schema validation

# Schemas
- Plugins have a schema attribute to replace validator() method. This attribute is the json schema describing their configuration.
- When plugins are registered, if they do not have a schema attribute, but do have a validator() method, we will add a property to the plugin which calls validator().schema() (for backwards compatibility purposes)
- We will add "title" and "decription" properties to all schemas (and subschemas) which can be used by a config editor for friendly labeling and mouseover help. These will default to just the key name of the dict they are in for backwards compatibilty. These could also possibly be used with error messaging, more below.
- We remove the LazyValidator type, and replace it by using $ref within schemas. We will use relative URIs, so in the case of using schemas provided by the REST api of the webui, it will be relative to the host flexget is running on. Snippet for a task would end up looking something like this:
```python
{
    "type": "object",
    "properties": {
        "accept_all": {"$ref": "/schemas/plugin/accept_all"}
        ...
    }
}
```
Possibly we also provide endpoints for dicts of plugins, so that a task schema just becomes:
```python
{"$ref": "/schemas/plugins/all"}
```
We could also provide endpoints for the set of plugins that only act on a certain phase. (or maybe it's better to classify all the plugins by their logical phase) We can then use something like the following within the "inputs" plugin schema:
```python
{
    "type": "array",
    "items": {"$ref": "/schemas/plugins/phase/input"}
}
```

- We will directly deference these during normal validation from the schema attribute added to plugins. (plus some helpers that build a dict validator of all plugins or plugins belonging to a certain phase etc.)
- These references will also be valid when accessed over http via the webui, because they will become relative to the host that served them, (this is part of json schema, we don't have to do anything,) and we'll flesh out the REST api for them to be served by a webui plugin.

# Errors
Errors need some thought as well. jsonschema provides us with a path to the problem very similar to what we already show (e.g. /tasks/atask/accept_all/), and in some cases has an error message very similar to what we already have. Other cases though the error messages will not be user friendly at all (e.g. "anyOf" validator will print the full schemas that needed to be matched.)
We need to come up with some way for cleaner user facing errors, possibly extend jsonschema with some sort of error keywords, haven't thought of anything really great yet though.

Came up with some ideas for this, a couple parts:
- I am adding more info to the exceptions that jsonschema gives us, which will be enough for us to create our own custom error messages. We'll be able to define our own errors for each of the validation keywords (e.g. in type validator, 'object' sucks when referring to a dict)
- For anyOf keywords, we'll be able to look at each of the errors from the subschemas, and try to determine the best course of action for which errors to show. This is still a tough problem if we can't figure out which form the user meant to be using, but that was a problem with the old validator as well, so at least it shouldn't get any worse.
- I'm thinking we also add an 'error' keyword, and/or 'error_xxx' keywords where xxx is the validation keyword that failed. Plugins could define these in their schemas to further customize errors for individual plugins. These would be ignored if the schema was used outside of our validator, but that shouldn't be as much of a problem, as if there is a config editor, it should be guiding input such that errors are less likely to begin with.


# Endpoints
Here's what I'm thinking for endpoints to get schemas:
- /schemas/plugin/<nameofplugin>: The schema for an individual plugin
- /schemas/plugins/all: A schema which allows all plugins in dict form, i.e. what a task accepts.
These would be dict validators, like all, but for a subset of plugins:
- /schemas/plugins/group/<groupname>
- /schemas/plugins/phase/<phasename>
- /schemas/plugins/context/<contextname>

I guess we should have an endpoint for getting the root schema as well
- /schemas/root

# Issues
Started implementing this [here](https://github.com/Flexget/Flexget/tree/jsonschema). Ran in to a couple issues so far.
- I removed the {"$ref": "/schema/plugins?context=input"} style refs for the moment in favor calling a function directly to create that schema.
This is an issue because when plugins are registered, the list of plugins is incomplete, so the generated schema is incomplete.
I'm thinking we add that back in by allowing functions to be passed to [register_schema](https://github.com/Flexget/Flexget/blob/jsonschema/flexget/config_schema.py#L13) which will be evaluated by [resolve_local](https://github.com/Flexget/Flexget/blob/jsonschema/flexget/config_schema.py#L17) when accessed. EDIT: Did this [here](https://github.com/Flexget/Flexget/commit/1d764c1d997457a34414871f9a3b8ca53ef29de8)
- Validating dict keys.
There are a couple spots where we validate dict keys. (regexp plugin allows only valid regexps as keys, if plugin makes sure keys don't contain some words)
Json schema only has methods to do this with regex. This will work for some of our current uses (if plugin) but not others (regexp). There are a few options:
We can define our own validation keywords, extending json schema. This may not be desirable if we want to be able to use our schemas in any external tools, like a config editor.
Relax some of the validation on these in favor of runtime errors.
Rethink the config format to avoid having to validate keys.
- Errors.
They suck right now. We need to come up with what our requirements are, and how best to display both general errors, and custom errors that can be defined by plugins.
- 'interval' and possibly other validators
The could be validated with the 'pattern' keyword, using the regex for a valid interval, this would mean other implementations can validate them. It would be much easier to add them to a plugin's schema if it is a custom 'format', as well as make it easier to give custom error messages about them. I think the latter is a better plan, but we'll have to figure how that works out (and our other custom formats) when used from a webui config editor.