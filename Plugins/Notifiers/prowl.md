# *Prowl*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Prowl can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

Send messages to your iPhone using [Prowl](http://prowlapp.com).
## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|api_key|text|User's API Key. Can also be a list. **Required**
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|application|text|The name of your application or the application generating the event|`FlexGet`
|provider_key|text|Optional	Your provider API key. Only necessary if you have been whitelisted
|priority|numeric| Set message priority. Values between -2 and 2 are accepted.| `0`|

### Example
Get your unique API key [here](/https://prowlapp.com/api_settings.php)

<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

```yaml
notify:
  entries:
    via:
      - prowl:
          api_key: <your apikey>
```
