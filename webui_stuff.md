{{{
<stevezau> so, i've written my own download manager, its been running for a little while now.. it uses flexget as its backbone.. i haven't shown it to anyone..
<gazpachoking> What's it do? :)
<stevezau> figured i'd show u if u want to see. as i'd eventually like to start working on a ui frontend for flexget that plugs into my d/l manager
<stevezau> 2 secs, phone rang
<stevezau> ok, http://-----------------
<stevezau> user: ------
<stevezau> pass: ------
<stevezau> so flexget listens to a bunch of rss feeds from private sites.. a custom plugin i wrote sends a notification to this app and adds it to the queue (sometimes pending depending on your flexget cofnig)
<stevezau> this app downloads, extracts and renames then notifys xbmc or plex
<gazpachoking> Hmmm, there is some awesome stuff there..
<stevezau> shows that are in your favs (config > approved shows) auto download.. any shows that is matched by a flexget rule.. maybe genre of doco or imdb rating between 6-7 or tvdb genre of reality (my wife lol)..
<gazpachoking> And now I've deleted all your downloads. muhahaha
<stevezau> it allows u to approve before it downloads.. once u approve it tells thetvdb favs.. so flexget will auto download without going to pending
<stevezau> haha
<gazpachoking> j/k ;)
<stevezau> i was worried about that :P
<stevezau> i havent implemented the permissions system properly
<stevezau> lol
<stevezau> also, lets say u add a show to config > approved show.. u can go to other > find missing (select the show)
<stevezau> it will show u the misses seasons/eps.. then by 1 click u can tell it to go find the missing eps and auto download them.. u can also manual search via other > manual search
<stevezau> so, the thing its missing is being able to change flexget config
<gazpachoking> That's some cool stuff.. the kind of stuff I wish the flexget webui could do natively now...
<stevezau> thats what i wanted to show u
<stevezau> trying to understand where u want to take the flexget gui
<gazpachoking> I don't really have a good plan
<stevezau> and if maybe we can built on it using what ive built
<gazpachoking> Been taking a bit of a break recently
<stevezau> ah yeah
<stevezau> it comes and goes in waves for me as well :)
<gazpachoking> But, pending queue sounds interesting for sure. And some sort of plugin to do some of the series things semi-manuall also sounds cool
<stevezau> do you see the gui eventually being a download manager
<gazpachoking> I haven't really envisioned it being a download manager, but I do like some of your ideas
<gazpachoking> What is doing the actual downloading in your app?
<stevezau> curl..
<stevezau> pycurl
<stevezau> so it can support ftp/http etc
<gazpachoking> A long time ago I envisioned a system where flexget would keep track of stuff it grabbed, and a webui plugin could be integrated with other download tools.
<stevezau> brb phone again
<gazpachoking> (specifically deluge, as that's what I use, but something more general would be the idea)
<gazpachoking> My theory was that in a given list of downloads, it could ask other flexget webui plugins for extra info, and e.g. a deluge webui plugin could supply things like download percentage
<gazpachoking> But I don't really have any thought out plan for how that could happen cleanly.
<gazpachoking> The deluge webui plugin would be a sort of glue, which when given events by flexget would ask deluge, and supply metainfo back.
<stevezau> yeah no support for torrents atm.. my server in the us downloads the torrents via rtorrent then serves them up via ftp and an rss feed.. flexget listens to that
<stevezau> i guess we could integrate with deluge
<gazpachoking> As well as maybe responding to some sort of other events, perhaps delete, which would both forget the thing in flexget, and hand off to external plugin, such as deluge, which would remove the actual download.
<gazpachoking> I'd want it to be some general event driven framework
<stevezau> yeah
<gazpachoking> So that whatever downloader you used, hopefully a (simple) integration plugin could be made.
<stevezau> and hooks for other downloaders like rtorrent
<gazpachoking> I started thinking it might get too complicated though. Never really planned it out far enough to imagine how it would work in practice.
<stevezau> downloader interface with start/stop/status/delete etc
<gazpachoking> Right right, like that.
<stevezau> i think its possible
<stevezau> we would need another plugin for post-processing.. extracting and renaming
<gazpachoking> Sometimes I get too general with my ideas, wanting it to be compatible with everything, which gets really complicated. Many different flexget apis to implement. But then again, I like the idea of keeping it general and extensible.
<stevezau> but then flexget becomes a proper media manager similar to sickbeard or couchpotato
<gazpachoking> Yeah, that would be pretty slick
<stevezau> well it's possible
<stevezau> we would just need to design the framework/layout 
<gazpachoking> Right. I have really dithered on most things webui, and haven't nailed anything down yet. Not super experienced in anything web or ui related.
<stevezau> and start with support for deluge/rtorrent (i can easily do rtorrent as it has xmlrpc interface)
<stevezau> me neither really.. i started this app about 4-5months ago
<stevezau> wrote it in php first.. then ported it to python using django
<gazpachoking> A step up. :P
<stevezau> haha yeah
<gazpachoking> We are using flask in the webui now, which I'm pretty happy with, but we need some sort of framework on top of it for flexget webui plugins, which I really am not sure how it should go.
<gazpachoking> And I haven't thought much about what it should do other than a config editor
<gazpachoking> Until this
<stevezau> i usually write in java.. this app made me learn python.. learnt alot :P
<stevezau> django make things really easy
<stevezau> ah ok, i havent looked at flask
<gazpachoking> I haven't used django too much, I think some stuff is quite similar, but my impression is that flask is a bit lighter and more modular.
<gazpachoking> Did your download just go from ~90 to ~30 percent? :P
<stevezau> lol oh u are still on there
<stevezau> umm
<stevezau> dont think so, unless it went to another d/l
<gazpachoking> I'll stop snooping. :P
<stevezau> lol
<stevezau> feel free to look around
<stevezau> http://stevez0.com:8000/ - were u looking at the 90% there?
<stevezau> thats how full my hdd is :P
<gazpachoking> Ahh, yup.
<stevezau> im watching u now.. searching for all in you eyes? :P
<stevezau> haha.. it got some xxx results
<gazpachoking> Yeah, just found that search tab
<gazpachoking> It suggested some good alternate films for you though.
<stevezau> the search is in alpha really :P
<gazpachoking> Hehehe
<stevezau> lol
<stevezau> u can do a find missing report as well..
<stevezau> shows u what eps u are missing
<gazpachoking> Yeah, just peeking theer too
<stevezau> this sorta stuff i dont think we should include in the flexget ui
<stevezau> maybe as a add-on
<gazpachoking> A separate searching plugin would be cool, that could inject or somesuch
<stevezau> yeah
<stevezau> so couchpotate and sickbeard are for all the people who dont have access to private torrent sites..
<stevezau> there is nothing for people who use private trackers.. 
<gazpachoking> Though a greasemonkey plugin might also be fine to link it over from external searches, ala couchpotato. (I think that's couchpotato works?)
<stevezau> flexget is what is mainly used but its not a media manager
<stevezau> yeah we could do that..
<stevezau> couchpotate and sickbeard both have api's
<gazpachoking> I do want a json api for flexget
<gazpachoking> Have a bit of a start on it
<stevezau> have u seen pyload before?
<stevezau> i stole this idea from an app called http://pyload.org/ 
<gazpachoking> I've heard of it, and perhaps even blindly changed some code in the flexget plugin, but not used it.
<stevezau> i stole their UI header lol.. i was going to have a chat with the owner but i think a flexget ui is the way to go
<stevezau> or maybe we can evolve pyload and my app into the flexget ui
<gazpachoking> Yes, looking at the plugin history, you'd think I know what pyload does... https://github.com/Flexget/Flexget/commits/develop/flexget/plugins/output/pyload.py
<gazpachoking> But, I don't. :P
<stevezau> haha
<stevezau> the more i think about this the more im liking the idea of FlexGet Media Manager..
<gazpachoking> I sorta like the idea of keeping the downloading separate, though I'll have to actually look at it to know fully what you mean. Ideally, there would be just a bit of minimal glue needed to connect the api of flexget with an external download manager.
<gazpachoking> But, sometimes I try to generalize things too much.
<gazpachoking> And then sometimes I just give up and do some hacky shit. :P
<stevezau> well thats exactly what i've already done.. so when flexget accepts an item my lazy plugin sends a json notification to my app
<stevezau> it then handles the d/l from there
<gazpachoking> Did you make an output plugin for flexget for that?
<stevezau> i just thought maybe we could evolve flexget into a proper media manager.. 
<stevezau> yep 
<stevezau> https://github.com/stevezau/lazy_client/blob/master/flexget-conf/plugins/lazy.py
<gazpachoking> Yeah, I'm torn between making a more integrated solution, but then not wanting to tie it down to one thing.
<stevezau> yeh
<stevezau> you own flexget right
<gazpachoking> And also not wanting the user to have to configre 10 parts to get everything configured.
<stevezau> does paranoidi part own it as well?
<gazpachoking> He made it, I joined later.
<stevezau> ah ok
<gazpachoking> But I've done a lot of work since then
<stevezau> well what im thinking is flexget-ui would become the new flexget
<stevezau> with the ui there would be no need for flexget command line
<gazpachoking> He has good design ideas though, if he has time for some input I think it would be quite valuable.
<gazpachoking> Much of what I have done comes from his ideas.
<stevezau> django has its own in-built web server.. so a user would download flexget.. unzip then simply ./flexget start (which loads the webserver.. then goes to http://ip:port/
<gazpachoking> I'm also torn about that, I very much like the cli
<gazpachoking> Have you tried current webui? Already does that bit.
<gazpachoking> 'flexget webui start' though.
<stevezau> ah yeah, i do recall it had that
<gazpachoking> But, there are not really many desirable features in the webui at the moment
<stevezau> ok well lets get paranoidi idea/thought on this.. ill prob need to show him my app for him to understand
<stevezau> yeah i know, thats why im talking to you right now :)
<gazpachoking> Yeah, that would be awesome. If we could get some sort of draft page with some good api plans that would be nice
<stevezau> yeah
<gazpachoking> I've got sorta frozen with indecision every time I try to work on webui stuff
<stevezau> before that i'd prefer to talk to paranoidi and yourself first... make sure this is the path you guys want to go
<stevezau> are u able to share this chat with paranoidi?? then i can give him login to look at my app
<stevezau> i've hardly spoken to him, don't think its appropriate coming from me :P
<gazpachoking> I can move it to a page here http://flexget.com/wiki/Drafts (minus your address/username/pass of course) and ping him. http://flexget.com/wiki/Drafts
<stevezau> yep thats fine
<stevezau> anyway, i've gota head out now. thanks for taking the time
<gazpachoking> It's public, so if you want to write any ideas, it might be easier to link them to us, and us back, since irc is largely async
<stevezau> i'll still idle in here for now on
<stevezau> yep, no problems with that
<stevezau> so you will post our chat in drafts and get paranoidi to take a look?
<gazpachoking> Hopefully ;)
<stevezau> ok, ill check back later with paranoidi to give him access to my app then we can all diccuss the idea
<gazpachoking> He, like I, has waxing and waning interests
<stevezau> heh
}}}