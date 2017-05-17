# [Notifiers](/Plugins/Notifiers) > RapidPush
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; RapidPush is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>
RapidPush is an easy-to-use push notification service for Android devices.  

To use this Plugin you need the Android application "RapidPush" which can be found within the [Google Play Store](https://play.google.com/store/apps/details?id=com.syncoorp.rapidpush).  
You need also an account at http://rapidpush.net .  
After you have logged in to your account, go to your user interface and click on the tab "API-Keys". Then create a new or use an already existing one with this Plugin.

You can now also use the channel feature, to send broadcast notifications to your subscribers.
## Configuration
| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. Can also be a list. **Required**
|group|text|Device group
|channel|text|Target channel
|priority|numeric| Set message priority. Values between 0 and 6 are accepted.|

#### Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

```yaml
notify:
  entries:
    via: 
      - rapidpush:
          priority: 3
          group: mydevices
          api_key: API_KEY
```

#### Example with multiple API-Key
```yaml
notify:
  entries:
    via: 
      - rapidpush:
          priority: 3
          group: mydevices
          api_key:
            - API_KEY1
            - API_KEY2
```