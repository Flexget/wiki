# [Notifiers](/Plugins/Notifiers) > Gotify
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Gotify is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin provides the ability to send flexget notifications via the self-hosted Gotify notification server (https://gotify.net).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**url**|URL|Gotify server URL **Required**|
| **token**| text| User's Gotify token. **Required**|
|priority|integer|Message priority. The Android client classifies messages by High (>7), Normal (4-7), Low (1-3) and Minimum priority (<1).|4

### Examples

### Send notification for each accepted entry
```yaml
    notify:
      entries:
        via:
          - gotify:
              url: <GOTIFY_SERVER_URL>
              token: <GOTIFY_TOKEN>
              priority: <PRIORITY>
```


