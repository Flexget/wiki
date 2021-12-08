# nzbget

### Example

```yaml
nzbget:
  url: http://nzbget:1234@localhost:6789/xmlrpc
  category: movies
```

### All possible parameters

```yaml
nzbget:
  url: ...
  category: ...
  priority: ...
  top: ...
```

## Override category

By setting [entry](/Entry) category you can override / specify nzbget category per item. To set it you can use plugins like [set](/Plugins/set), [manipulate](/Plugins/manipulate). top stands for append to top, each nzb will be added to the top of the queue. Further you can modify the Priority which is used for a file by nzbget with the priority parameter, the valid values are -100 (lowest) to 100 (highest). More information can be found in the [[API reference](http://nzbget.sourceforge.net/RPC_API_reference#Method_.22appendurl.22|RPC)].

See [this recipe](/Cookbook/Series/SeriesSabNZBd) for example how to set category from a series name.