= Web UI =

To pull the webui dependencies, use `pip install flexget[webui]` when installing. Experimental web-ui can be started with `flexget webui` command, see `flexget webui --help` for default port and usernames and options for setting them.

'''NOTES:'''
- You will lose the formatting of your config file if you edit it through the web-ui.
- Remember to exit the web-ui if you have cron scheduled to run flexget normally. Otherwise the web-ui lock file will interfere.

'''More motivated python capable web-ui developers are needed! '''

Some mockup plans [https://flexget.mybalsamiq.com/projects]

Join our irc-channel to participate in the project! The technology stack behind the webui is flask, jinja2 and cherrypy as server.
Here are a couple of drafts for things we would like to work on in the webui:
- Drafts/ConfigEditor A fully featured editor for config files.
- Drafts/RecipeRepository A simpler system to set up config by picking a template and filling in key values.

= Steve's Media Manager =
I've built app that allows you to manage your downloads and media. Flexget directly feeds the app.

It's built using the same plugin/addon architecture as flexget. Plugins can register new events and download phases as required. They also can register new pages on the UI and ui_events.. such as ui_header_links..

I'd like to take what I've done and integrate/build-up the flexget UI. I know flexget is not designed to be a media manager but if the ui is designed with an event/plugin driven architecture then i can create an add-on called FlexMedia which includes the downloading via rtorrent/utorrent, extracting, auto renaming using tvdb/imdb, find missing episodes, auto find best quality of movie (via providers.. trackers) etc..

I think this would be a great addition to flexget and from what i've seen would be valuable to many people. The other alternative media managers out there are no where near flexible as flexget..

Below I've outlined its current design. '''bold'''Obviously need to re-design to fix with flexget.'''bold'''

''' Flow '''
1. Flexget accepts an entry and forwards to entry to the media manager API
2. API creates download in database with title, link etc from flexget.
3. The queue manager detects the newly added download and kicks off the processor.
4. Processor runs the download through each of the phases (starting from it's current phase).
- Each phase calls event on_download_<phase> which returns all the associated methods.. It executes the methods in order of priority (Same way flexget does)
- Plugins at any stage can halt a phase (setting it to wait).. IE: the torrent plugin will fw the .torrent onto rtorrent via it's scgi/http then call for the download to halt on event on_download. The torrent plugin has registered a @cron which is triggered every 5mins to check for completion, once complete it changes the phase status to ready and the queue manager resumes running the download through each phase.

[[Image(Flow.png)]]

''' UI '''

[[Image(UI.png)]]