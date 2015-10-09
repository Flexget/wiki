= Web UI =

Development has started on a web interface for managing flexget.

'''We need your help! If are an AngularJS developer or can help with the layout/design then please join in the effort! '''

For development you will need NPM [https://nodejs.org/en/]

To install the webui dependencies run "npm update" in the folder <git clone>/flexget/ui

Add the following to your config.yml


{{{
web_server:
  bind: 0.0.0.0
  port: 5050
api:
  username: flexget
  password: flexget
webui: yes
}}}

UI will be avaliable at [http://flexget_host:5050/ui/]

API will be avaliable at [http://flexget_host:5050/api/]

'''NOTES:'''
- You will lose the formatting/order of your config file if you edit it through the web-ui.
- The UI communicates with Flexget via the API. Browse to [http://flexget_host:5050/api/] for the documentation


'''Plugins:'''

The web interface uses AngularJS with a pluggable architecture. Each plugin requires a plugin.json with a name a version set as a minimum. See examples here [https://github.com/Flexget/Flexget/tree/develop/flexget/ui/plugins]
[[BR]]
[[BR]]


Join our irc-channel to participate in the project! The technology stack behind the webui is angularJS.
Here are a couple of drafts for things we would like to work on in the webui:
- Drafts/ConfigEditor A fully featured editor for config files.
- Drafts/RecipeRepository A simpler system to set up config by picking a template and filling in key values.

'''TODO:'''

- Bind to interface vs ip
- Authorization system 
- Store users in database
- Store sessions in database (so remember me works after restart of flexget)
- Manage users/passwords via UI
- Build plugin history
- Build plugin execute
- update plugin log, make more user friendly
- Build plugin scheduler
- Build plugin tasks


