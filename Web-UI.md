= Web UI =

'''We need your help! If are an AngularJS developer or can help with the layout/design/css then please join in the effort! (See Development Section Below)'''

'''Relevant pages'''

* [https://flexget.mybalsamiq.com/projects UI mockups] - accounts can be requested
* [wiki:Web-UI/Concepts Concepts]
* [wiki:Roadmap Roadmap (more ideas)]

Development has started on a web interface for managing flexget. To enable add the following to your config.yml

{{{
web_server:
  bind: 0.0.0.0
  port: 3539
api: yes
webui: yes
}}}

Set a password and start flexget in daemon mode to start the web server.

{{{
flexget web passwd <some_password>
flexget daemon start --daemonize
}}}

Flexget UI will be available at http://flexget_ip:3539/ui/

Full API documentation will be available at http://flexget_ip:3539/api/


== Authentication ==
The login username is `flexget` and the password is what you set above.

You can also use an authorization header to access the API with the following format: `Authorization: Token <TOKEN>`

You can view the API token using the following commands

{{{
# View token
flexget web showtoken

# Generate new token
flexget web gentoken
}}}

'''NOTES:'''
- You will lose the formatting/order of your config file if you edit it through the web-ui.
- The UI communicates with Flexget via the API. Browse to http://flexget_ip:3539/api/ for the documentation


== Development ==

We have a functional API with documentation available at http://flexget_ip:3539/api/.

The UI has a solid base but we need help building the plugins. If you would like to get your hands dirty in AngularJS, CSS or UX Design then please read below and join our chat at gitter [https://gitter.im/Flexget/Flexget]

To get started you will first need to setup your environment from Git.

=== Setup from Git ===

You will need to install NPM (see [https://nodejs.org/en/])

Following commands will do that as user, requires g++ to be installed:

{{{
echo 'export PATH=$HOME/local/bin:$PATH' >> ~/.bashrc
. ~/.bashrc
mkdir ~/local
mkdir ~/node-latest-install
cd ~/node-latest-install
curl http://nodejs.org/dist/node-latest.tar.gz | tar xz --strip-components=1
./configure --prefix=~/local
make install # ok, fine, this step probably takes more than 30 seconds...
curl -L https://www.npmjs.org/install.sh | sh
}}}

Alternative NPM installation (untested)

{{{
# install node wherever.
# use sudo even, it doesn't matter
# we're telling npm to install in a different place.

echo prefix = ~/local >> ~/.npmrc
curl https://www.npmjs.org/install.sh | sh
}}}

Install bower and gulp. This needs to be ran as root except if you installed NPM as user with previous commands.

{{{
npm install -g bower
npm install -g gulp
}}}

Next install the webui dependencies by running the following commands under the <flexget github folder>/flexget/ui folder.

{{{
npm install
bower update
gulp build
}}}

Running `gulp build` will compile all the ui files.

=== Running from Git ===

The UI communicates to the flexget daemon using the API. When starting the daemon it will make the ui available via http://flexget_ip:3539/ui/.

The daemon will load the compiled UI files if you are NOT in debug mode. To enable debug mode run

{{{
flexget -L debug daemon start
}}}

''' Plugin development from Git'''

For plugin development see examples here [https://github.com/Flexget/Flexget/tree/develop/flexget/ui/plugins] and also feel free to chat with us on gitter [https://gitter.im/Flexget/Flexget]

To make development easy we are using browserify so when you change a file it will be automatically refreshed on your browser. To get this working you will need to start the flexget daemon (as above). Then you can run

{{{
#option 1: run ui using local flexget daemon
gulp serve

#option 2: run UI against a different flexget server
gulp serve --server <flexget_api:port>
}}}

== Testing ==

We have recently started adding tests to our existing parts of the UI. Currently they reside in a PR [https://github.com/Flexget/Flexget/pull/1206] until the refactoring and setting up is done.

The tests can be run be using {{{ karma start }}} or {{{ npm test }}} commands in the UI folder (/flexget/ui).

There is also a browser version available that can be started by using {{{ gulp serve-specs }}}, this will open a web browser to the address {{{ localhost:5050 }}} in which all the tests are compiled and ran. Selecting a subsection of the tests will allow you to filter down and only run the tests you want to focus on.

The frameworks currently used for the tests are:[[BR]]

- Karma: [http://karma-runner.github.io/0.13/index.html]
- Mocha: [https://mochajs.org]
- Sinon: [http://sinonjs.org]
- Chai: [http://chaijs.com]
- Bardjs: [https://github.com/wardbell/bardjs]

If you have any more questions regarding testing of the different parts and modules of the UI, you can ask them in our Gitter chat [https://gitter.im/Flexget/Flexget]