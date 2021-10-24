# Log Filter

<div class="alert alert-warning" role="warning">
  <span class="glyphicon glyphicon-exclamation-sign"></span>
  &nbsp; Do not use this plugin if you are attempting to get support. Lines missing from the log can make debugging harder, even if they are unrelated to the problem.
</div>

This plugin will disable certain messages from the log. It can be used if there is a particularly chatty plugin which is filling up your logs. Consider changing your log level, or sending a PR to improve the logging of problem plugins before using this plugin though.
## Config format
```yaml
log_filter:
- message: "subset of text contained in log message to be filtered"
  # The following properties are optional, in order to improve specificity of which log messages to filter
  plugin: name of plugin producing the message
  level: log level of unwanted message
```