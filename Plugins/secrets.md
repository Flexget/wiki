# Secrets

<div class="alert alert-danger" role="info">
  
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp; This plugin was renamed in version 2.9.0. The secrets plugin is now the [variables](/Plugins/variables) plugin.
</div>


Born to strip off passwords, api keys and other sensitive info from the configuration file, this plugin basically processes some jinja2 templates on startup to assign the corresponding values set in a dedicated yaml file or from DB.
All the templates to process must begin with the word "secrets".

### Example
In this sample `config.yml` we configure the plugin to look for config secrets in a file named `secrets.yml`:

```yaml
secrets: secrets.yml
templates:
  tell_me:
    notify_xmpp:
      sender: '{{ secrets.xmpp.usr }}'
      password: '{{ secrets.xmpp.pwd }}'
      recipient: some@recipient.xyz
      title: 'something new: {{ title }}'
tasks:
  test:
    template:
      - tell_me
    trakt_list:
      username: '{{ secrets.a_long.time_ago }}'
      password: '{{ secrets.a_long.in_a_galaxy }}'
      list: test
      type: movies
```

And this is the `secrets.yml` content:

```yaml
xmpp:
  usr: xxx@yyy.zzz
  pwd: mypassword
a_long:
  time_ago: xxx
  in_a_galaxy: yyy
  far:
    far:
      away: zzz
```

So this will be the resulting `config.yml` before executing tasks:

```yaml
secrets: secrets.yml
templates:
  tell_me:
    notify_xmpp:
      sender: 'xxx@yyy.zzz'
      password: 'mypassword'
      recipient: some@recipient.xyz
      title: 'something new: {{ title }}'
tasks:
  test:
    template:
      - tell_me
    trakt_list:
      username: 'xxx'
      password: 'yyy'
      list: test
      type: movies
```
#### Secrets from DB
Secrets can be also cached to and loaded from DB (starting in v2.1.11). From that version, if a secrets file is present in configuration file, its contents will be cached to DB and will be accesible via the `/secrets/` endpoint in the API.

In order to have the config use the secrets from the DB instead of the file, use `secrets: yes` in the config file instead of the secret file name. Loading secrets from DB and not the file is recommended when using the WebUI/API

### Notes
- Key name have limited support for special characters (at least "-" is not working). Stick with letters and underscore.
- The secrets file must stay in the same config.yml location.
- Use singles quotes around URLs in your `secrets.yml` file.
- Any template the plugin cannot process, for any reason (i.e.: a template not starting with "secrets" or missing in the secrets file) will be ignored.
