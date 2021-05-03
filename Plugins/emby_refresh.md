# Trigger Emby Refrsh
This plugin triggers a emby refresh

## Plugin Settings
Currently the following settings are supported:

| Option| Description |
| --- | --- |
| **host** | The emby host, including `protocol` and `port` |
| **username** | The `username` of the user, should be provided with `password` or with a `apikey`. If a `apikey` is informed, the user can be any user in the server, if a `password` is informed, the login `username` plus `password` must match |
| **password** | The `password` to authenticate the `username`  |
| **apikey** | The apikey to use to authenticate |
| **when** | When to `refresh`, on `accepted`, `rejected`, `failed`, `no_entries`, `aborted`, `always`

## Config format
```text
emby_refresh:
    server:
        host: http://localhost:8096
        username: <username>
        [apikey]: <apikey>
        [password]: <password>
        [return_host]: <wan|lan>
    [when]: <accepted|rejected|failed|no_entries|aborted|always>
```

## Examples
```yaml
emby_refresh:
  server:
    host: http://emby.localhost:8096
    username: flexget
    password: flexget
    return_host: wan
  when: accepted
```