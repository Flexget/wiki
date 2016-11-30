# Email

<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Email can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

The email plugin can be used to notify you of task results and/or failures. There are two built in templates, or you can make your own template using the Jinja2 templating language.

The `default` template will notify you of all downloaded entries, and of any failed entries or task aborts. There is also an included `failed` template to just notify when there are problems with a task.

## Config

| Attribute |  Description | 
| --- |  --- | 
| to |  The email address(es) of the recipient(s). **Required.**
| from|  The email address from which the email will be sent. Default is`flexget_notifer@flexget.com` | 
| title | The subject for the email| 
| message | The message body| 
| smtp_host | The host of the smtp server. Default is `localhost`| 
| smtp_port | The port of the smtp server. Default is `25`| 
| smtp_username | The username to use to connect to the smtp server| 
| smtp_password | The password to use to connect to the smtp server| 
| smtp_tls | Should TLS be used to connect | 
| smtp_ssl | Should SSL be used to connect| 
| file_template | Name of the template file to use| 




### Built-In Templates

- `default`: This will send emails with a list of accepted entries, and/or a list of failed entries. (this template is used automatically if you do not specify one.)  
- `failed`: This will only send emails when there are entries that have failed.
- `accepted`: This will only send emails about accepted entries.
- `html`: This attempts to make html formatted emails with images for series and movies.

### Custom Templates
You can create your own custom templates for the email plugin in the jinja2 templating language. They should be placed in <configpath>/templates, and their filename specified as the `template` option. See the [default template](https://github.com/Flexget/Flexget/blob/master/flexget/templates/email/default.template) for an example.

### Examples
**Config basic example**

```yaml
email:
  from: xxx@xxx.xxx
  to: xxx@xxx.xxx
  smtp_host: smtp.host.com
```

**Config example with smtp login and multiple recipients**

```yaml
email:
  from: xxx@xxx.xxx
  to:
    - xxx@xxx.xxx
    - yyy@yyy.yyy
  smtp_host: smtp.host.com
  smtp_port: 25
  smtp_username: my_smtp_login
  smtp_password: my_smtp_password
```

**Config multi-task example using the failed template**
A single email will be sent with only the failures from any of the tasks except for task3, where it is turned off.

```yaml
email:
  from: xxx@xxx.xxx
  to: xxx@xxx.xxx
  smtp_host: smtp.host.com
  template: failed

tasks:
  task1:
    rss: http://xxx
  task2:
    rss: http://yyy
  task3:
    rss: http://zzz
    email:
      active: False
```

**Gmail example**
```yaml
email:
  from: from@gmail.com
  to: to@gmail.com
  smtp_host: smtp.gmail.com
  smtp_port: 587
  smtp_username: gmailUser
  smtp_password: gmailPassword
  smtp_tls: yes
```