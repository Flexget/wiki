# Web UI
**We need your help! If you are an AngularJS developer or can help with the layout/design/css then please join in the effort! (See Development Section Below)**

**Relevant pages**

* [UI mockups](https://flexget.mybalsamiq.com/projects) - accounts can be requested
* [Concepts](/Web-UI/Concepts)
* [Roadmap (more ideas)](/Roadmap)

Development has started on a web interface for managing flexget. To enable add the following to your config.yml

```
web_server:
  bind: 0.0.0.0
  port: 3539
  ssl_certificate: '/etc/ssl/private/myCert.pem'
  ssl_private_key: '/etc/ssl/private/myKey.key'
api: yes
webui: yes
```

Set a password and start flexget in daemon mode to start the web server.

```
flexget web passwd <some_password>
flexget daemon start --daemonize
```

Flexget UI will be available at http://flexget_ip:3539/ui/

Full API documentation will be available at http://flexget_ip:3539/api/


## Authentication
The login username is `flexget` and the password is what you set above.

You can also use an authorization header to access the API with the following format: `Authorization: Token <TOKEN>`

You can view the API token using the following commands

```
# View token
flexget web showtoken

# Generate new token
flexget web gentoken
```

**NOTES:**
- You will lose the formatting/order of your config file if you edit it through the web-ui.
- The UI communicates with Flexget via the API. Browse to http://flexget_ip:3539/api/ for the documentation


## Development
We have a functional API with documentation available at the `/api` route of your web server. <br>
Example: [http://localhost:3539/api/](http://localhost:3539/api/) .

The UI has a solid base but we need help building the plugins. If you would like to get your hands dirty in AngularJS, CSS or UX Design then please read below and join our chat at gitter [https://gitter.im/Flexget/Flexget](https://gitter.im/Flexget/Flexget)

To get started you will first need to setup your environment from Git.

### Setup from Git

1. You will need to install NPM (see [https://nodejs.org/en/](https://nodejs.org/en/))

2. Following commands will do that as user, requires g++ to be installed:

```
echo 'export PATH=$HOME/local/bin:$PATH' >> ~/.bashrc
. ~/.bashrc
mkdir ~/local
mkdir ~/node-latest-install
cd ~/node-latest-install
curl http://nodejs.org/dist/node-latest.tar.gz | tar xz --strip-components=1
./configure --prefix=~/local
make install # ok, fine, this step probably takes more than 30 seconds...
curl -L https://www.npmjs.org/install.sh | sh
```

Alternative NPM installation to virtualenv (untested)

```
$ curl http://nodejs.org/dist/node-latest.tar.gz | tar xvz
$ cd node-v*
$ ./configure --prefix=$VIRTUAL_ENV
$ make install
```

Alternative NPM installation (untested)

```
# install node wherever.
# use sudo even, it doesn't matter
# we're telling npm to install in a different place.

echo prefix = ~/local >> ~/.npmrc
curl https://www.npmjs.org/install.sh | sh
```

3. Install bower and gulp. This needs to be ran as root except if you installed NPM as user with previous commands.

```
npm install -g bower
npm install -g gulp
```

4. Next install the webui dependencies by running the following commands under the <flexget github folder>/flexget/ui folder, or run `python dev_tools.py build_webui`.

```
npm install
bower update
gulp build
```
Running `gulp build` will compile all the ui files.




### Running from Git
The UI communicates to the flexget daemon using the API. When starting the daemon it will make the ui available via http://flexget_ip:3539/ui/.

The daemon will load the compiled UI files if you are NOT in debug mode. To enable debug mode run

```
flexget -L debug daemon start
```

### Plugin development from Git

For plugin development see examples here [https://github.com/Flexget/Flexget/tree/develop/flexget/ui/plugins](/https://github.com/Flexget/Flexget/tree/develop/flexget/ui/plugins) and also feel free to chat with us on gitter [https://gitter.im/Flexget/Flexget](/https://gitter.im/Flexget/Flexget)

To make development easy we are using browserify so when you change a file it will be automatically refreshed on your browser. To get this working you will need to start the flexget daemon (as above). Then you can run

```
#option 1: run ui using local flexget daemon
gulp serve

#option 2: run UI against a different flexget server
gulp serve --server <flexget_api:port>
```

## Testing
We have recently started adding tests to our existing parts of the UI. There are about 250 tests currently present. If you modify/add parts of the UI, ensure to also modify/add tests for the relevent changes (at least most of them).

The tests can be run be using a number of commands: 
```
#Option 1: Standard command line
karma start

#Option 2: Starting a web browser to run the tests in*
gulp serve-specs

#Option 3: Shorthand for the browser command
npm test
```

*: This gulp task watches for file changes, not file additions, after adding a new test file, thise task needs to be restarted.

All of these command need to be run inside the /flexget/ui folder.

When using the gulp task, a browser should open by itself, if it does not, you can navigate to `localhost:5050` where the tests will be avaiblable.

Results of the tests (that are run on the develop branch), can we viewed here: http://ci.flexget.com/job/Test-UI/

The frameworks currently used for the tests are:  

- Karma: [http://karma-runner.github.io/0.13/index.html](/http://karma-runner.github.io/0.13/index.html)
- Mocha: [https://mochajs.org](/https://mochajs.org)
- Sinon: [http://sinonjs.org](/http://sinonjs.org)
- Chai: [http://chaijs.com](/http://chaijs.com)
- Bardjs: [https://github.com/wardbell/bardjs](/https://github.com/wardbell/bardjs)

If you have any more questions regarding testing of the different parts and modules of the UI, you can ask them in our Gitter chat [https://gitter.im/Flexget/Flexget](/https://gitter.im/Flexget/Flexget)
### Attachments
* [Flow.png](/attachments/Web-UI/Flow.png)
* [UI.png](/attachments/Web-UI/UI.png)