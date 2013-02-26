Ideas for how to incorporate json schema validation

= Schemas =
- Plugins have a schema attribute to replace validator() method. This attribute is the json schema describing their configuration.
- When plugins are registered, if they do not have a schema attribute, but do have a validator() method, we will add a property to the plugin which calls validator().schema() (for backwards compatibility purposes)
- We will add "title" and "decription" properties to all schemas (and subschemas) which can be used by a config editor for friendly labeling and mouseover help. These will default to just the key name of the dict they are in for backwards compatibilty. These could also possibly be used with error messaging, more below.
- We remove the !LazyValidator type, and replace it by using $ref within schemas. We will use relative URIs, so in the case of using schemas provided by the REST api of the webui, it will be relative to the host flexget is running on. Snippet for a task would end up looking something like this:
{{{
#!python
{
    "type": "object",
    "properties": {
        "accept_all": {"$ref": "/schemas/plugin/accept_all"}
        ...
    }
}
}}}
Possibly we also provide endpoints for dicts of plugins, so that a task schema just becomes:
{{{
#!python
{"$ref": "/schemas/plugins/all"}
}}}
We could also provide endpoints for the set of plugins that only act on a certain phase. (or maybe it's better to classify all the plugins by their logical phase) We can then use something like the following within the "inputs" plugin schema:
{{{
#!python
{
    "type": "array",
    "items": {"$ref": "/schemas/plugins/phase/input"}
}
}}}

- We will directly deference these during normal validation from the schema attribute added to plugins. (plus some helpers that build a dict validator of all plugins or plugins belonging to a certain phase etc.)
- These references will also be valid when accessed over http via the webui, because they will become relative to the host that served them, (this is part of json schema, we don't have to do anything,) and we'll flesh out the REST api for them to be served by a webui plugin.

= Errors =
Errors need some thought as well. jsonschema provides us with a path to the problem very similar to what we already show (e.g. /tasks/atask/accept_all/), and in some cases has an error message very similar to what we already have. Other cases though the error messages will not be user friendly at all (e.g. "anyOf" validator will print the full schemas that needed to be matched.)
We need to come up with some way for cleaner user facing errors, possibly extend jsonschema with some sort of error keywords, haven't thought of anything really great yet though.

= Endpoints =
Here's what I'm thinking for endpoints to get schemas:
- /schemas/plugin/<nameofplugin>: The schema for an individual plugin
- /schemas/plugins/all: A schema which allows all plugins in dict form, i.e. what a task accepts.
These would be dict validators, like all, but for a subset of plugins:
- /schemas/plugins/group/<groupname>
- /schemas/plugins/phase/<phasename>
- /schemas/plugins/context/<contextname>

I guess we should have an endpoint for getting the root schema as well
- /schemas/root

