# Abort If Exists
Abort the running task if the specified field in an entry matches the regexp.

```YEXT
abort_if_exists:
  regexp: <regexp>
  field: <field name>
```
### Example

Abort the task if [lftp](https://lftp.yar.ru/) is currently transferring data. 

```yaml
filesystem:
  path:
    - /storage/movies/
    - /storage/tv/
  recursive: yes
  retrieve: files
  regexp: '.*\.(avi|mkv|mp4|lftp-get-status)$'
abort_if_exists:
  regexp: '.*\.lftp-get-status$'
  field: location
```