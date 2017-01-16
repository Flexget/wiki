# *Email*

<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Email can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

The email plugin can be used to notify you of task results and/or failures. There are two built in templates, or you can make your own template using the Jinja2 templating language.

The `default` template will notify you of all downloaded entries, and of any failed entries or task aborts. There is also an included `failed` template to just notify when there are problems with a task.

## Config

| Options |Type|  Description | Default |
| --- | ---| --- |---|
| to | email| The email address(es) of the recipient(s). **Required.**
| from| email| The email address from which the email will be sent. |`flexget_notifer@flexget.com` | 
| smtp_host | text|The host of the smtp server. |`localhost`| 
| smtp_port |numeric| The port of the smtp server. | `25`| 
| smtp_username |text| The username to use to connect to the smtp server| 
| smtp_password |text| The password to use to connect to the smtp server| 
| smtp_tls |yes/no| Should TLS be used to connect | no|
| smtp_ssl | yes/no|Should SSL be used to connect| no
|html| yes/no | Should parse message as HTML|no




### Built-In Templates

- `default`: This will send emails with a list of accepted entries, and/or a list of failed entries. (this template is used automatically if you do not specify one.)  
- `failed`: This will only send emails when there are entries that have failed.
- `accepted`: This will only send emails about accepted entries.
- `html`: This attempts to make html formatted emails with images for series and movies.

### Custom Templates
You can create your own custom templates for the email plugin in the jinja2 templating language. They should be placed in `/templates` in config path, and their filename specified as the `file_template` option. See the [default template](https://github.com/Flexget/Flexget/blob/master/flexget/templates/email/default.template) for an example.

### Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>
**Config basic example**

```yaml
notify:
  task:
    template: html  # Optional, if you want html instead of plain text
    via:
      - email:
          from: xxx@xxx.xxx
          to: xxx@xxx.xxx
          smtp_host: smtp.host.com
```

**Config example with smtp login and multiple recipients**

```yaml
notify:
  task:
    template: html  # Optional, if you want html instead of plain text
    via:
      - email:
          from: xxx@xxx.xxx
          to:
            - xxx@xxx.xxx
            - yyy@yyy.yyy
          smtp_host: smtp.host.com
          smtp_port: 25
          smtp_username: my_smtp_login
          smtp_password: my_smtp_password
```
**Gmail example**
```yaml
notify:
  task:
    template: html  # Optional, if you want html instead of plain text
    via:
      - email:
          from: from@gmail.com
          to: to@gmail.com
          smtp_host: smtp.gmail.com
          smtp_port: 587
          smtp_username: gmailUser
          smtp_password: gmailPassword
          smtp_tls: yes
```