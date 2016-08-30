# Max Reruns

Simple plugin that limits the number of reruns a specific task is allowed to perform consecutively. Useful for limiting the number of reruns [discover](discover) performs.

Example:

```YAML
  download-task:
    discover:
      what:
        - next_series_episodes: yes
      from:
        - some_search_plugin: yes
    max_reruns: 3
```