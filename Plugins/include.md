# Include
Allows including configuration from another file into a task.

### Example

**config.yml**

```
tasks:
  stuff:
    rss: ...
    include: series.yml
    download: ~/downloads/
```

**series.yml**

```
series:
  - foo
  - bar
```

This allows parts of configuration to be shared between multiple configuration files (databases).

You can also include multiple files using this format:
```
include:
  - include1.yml
  - include2.yml
```