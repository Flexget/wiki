# Web UI v2

<div class="alert alert-danger" role="alert">

  <span class="glyphicon glyphicon glyphicon-exclamation-sign"></span>
  &nbsp;
  Web UI is currently experimental and _is not_ recommended for new users!
</div>

<div class="alert alert-info" role="alert">

  <span class="glyphicon glyphicon glyphicon-comment"></span>
  &nbsp;
  We need your help! If you are a React developer or can help with the layout/design/css then please join in the effort.
</div>

**Related pages**

* [Repo](https://github.com/flexget/webui)
* [UI mockups](https://flexget.mybalsamiq.com/projects) - accounts can be requested
* [Concepts](/Web-UI/Concepts)
* [Roadmap (more ideas)](/Roadmap)
* [Github Status Issue](https://github.com/Flexget/webui/issues/42)
* [API](/API)
* [Web UI v1](/Web-UI/v1)

## Enabling Web UI

The web UI is enabled by placing the `web_server` key in your configuration file. SSL is optional, but it is highly recommended if the UI is exposed to the internet.

Note that `web_server` is one of a handful of [top-level keys](/Configuration#top-level-keys) in the configuration file. Do not indent `web_server`.

### `web_server` Usage 
This is the simple configuration that uses default values. It will enable the API and web UI at `http://0.0.0.0:5050/v2` (IP `0.0.0.0`, port `5050`) by default.
```yaml
web_server: yes
```

You can also set a different port using an alternate simple configuration mode. (**NOTE**: This simple mode will currently default to WebUI v1.)
```yaml
web_server: 8080
```
<br>

#### All configuration options
- `bind`: IP address to bind to
- `port`: Port at which the web UI and API will be accessed
- `ssl_certificate`: Path to certificate file
- `ssl_private_key`: Path to private key file
- `web_ui`: `yes|no` Set to no to disable the web UI; only the API will run
- `base_url`: Set a different base_url; default is `/`
- `run_v2`: Enable V2 UI. **Note:** This is subject to change.

Fully configured example:
```YAML
web_server:
  bind: 0.0.0.0
  port: 3539
  ssl_certificate: '/etc/ssl/private/myCert.pem'
  ssl_private_key: '/etc/ssl/private/myKey.key'
  web_ui: yes
  base_url: /foo
  run_v2: yes
```

## Starting Web UI
Set a password and start FlexGet in daemon mode to start the web server.

```bash
$ flexget web passwd <some_password>
$ flexget daemon start --daemonize
```

Using the full configuration example above, the Flexget Web UI would now be available at `http://flexget_ip:3539/v2`. Full API documentation would be available at `http://flexget_ip:3939/api/`.

Visit the [API page](/wiki/API) for more information about it.


## Authentication
The login username is `flexget` and the password is what you set using the `web passwd` command above.

You can also use an authorization header to access the API with the following format: `Authorization: Token <TOKEN>`

You can view or reset the API token using the following [CLI](/CLI/web) commands:

```bash
# View token
flexget web showtoken

# Generate new token
flexget web gentoken
```

## Sections currently working

## Development
The UI has a solid base but we need help building the plugins. If you would like to get your hands dirty in React, CSS or UX Design then please join our chat on [Gitter](https://gitter.im/Flexget/Flexget) and checkout the [CONTRIBUTING.md](https://github.com/Flexget/webui/blob/develop/.github/CONTRIBUTING.md) for getting setup and feel free to ask any questions in chat. 

### Attachments
* [Web UI Flow](/attachments/Web-UI/Flow.png)
* [UI](/attachments/Web-UI/UI.png)