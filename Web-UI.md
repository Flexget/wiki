= Web UI =

Experimental web-ui can be started with `flexget-webui` command, see `flexget-webui --help` for default port and usernames and options for setting them.

'''More motivated python capable web-ui developers are needed! '''

Join our irc-channel to participate in the project! The technology stack behind the webui is flask, jinja2 and cherrypy as server.

'''NOTES:'''
- You will lose the formatting of your config file if you edit it through the web-ui.
- Remember to exit the web-ui if you have cron scheduled to run flexget normally. Otherwise the web-ui lock file will interfere.