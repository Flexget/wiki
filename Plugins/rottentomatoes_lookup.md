= Rotten Tomatoes lookup =

Performs Rotten Tomatoes search for all entries in the feed and provides Rotten Tomatoes lookup functionality to other plugins.

Usually you don't need this, unless you know what you're doing :)

Example:

{{{
rottentomatoes_lookup: yes
}}}

'''{{{NOTICE:}}}''' With the shared api key included with !FlexGet, rate limiting can be a problem, causing lookups to fail. You can sign up for your own api key [http://developer.rottentomatoes.com/ here]. And specify it in the config:
{{{
rottentomatoes_lookup: XXXXXXXXXXXXXXXX
}}}