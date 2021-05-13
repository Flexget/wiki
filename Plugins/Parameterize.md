# Parameterize

<div class="alert alert-danger" role="info">
  
  <span class="glyphicon glyphicon glyphicon-alert"></span>
  &nbsp; This is a very advanced plugin. If you don't understand it, you probably don't need it, or want to be bothered trying to get it working. Proceed with caution.
</div>

This allows the config for an input plugin to be parameterized using another input plugin.

## Configuration

```yaml
parameterize:
  plugin:
    # Here you will include the plugin to be configured3
    # Any configuration setting which should be dynamic
    # can use Jinja to reference entry fields from the entries
    # produced by the plugin in the 'using' part of the config.
    plugin_to_be_configured: "{{parameterized_config_value}}"
  using:
    # This is the input plugin which will produce the dynamic
    # config values for use in the above 'plugin' section.
    some_input_plugin: config_here
```

### Example
This plugin can probably best be explained with an example. If you have a list of urls for rss feeds in a csv file, and want to use the [rss](/Plugins/rss) plugin to fetch all of those feeds, the parameterize plugin can accomplish that with the following.

```yaml
parameterize:
  plugin:
    rss: "{{url}}"
  using:
    csv: /my/list_of_rss_feeds
```