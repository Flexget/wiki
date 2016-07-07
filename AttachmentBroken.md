# For some reason Trac doesn't like to accept attachments

If you know how to fix this, please DO contact.

**Apache: sites-enabled/flexget.com.conf**

```
<VirtualHost *>
        ServerName flexget.com
        CustomLog /var/log/apache2/flexget.com-access.log combined

        WSGIScriptAlias / /var/trac/flexget/apache/cgi-bin/trac.wsgi

# 
#  NOTE: WHAT IS THIS? Makes no difference to anything
#
#        <Directory /var/trac/flexget/apache>
#            WSGIApplicationGroup %{GLOBAL}
#            Order deny,allow
#            Allow from all
#        </Directory>

</VirtualHost>

```

**TRAC.ini**

```
# -*- coding: utf-8 -*-

[account-manager](/account-manager)
force_passwd_change = true
hash_method = HtPasswdHashMethod
password_file = /var/trac/flexget/htpasswd.trac
password_format = htpasswd
password_store = HtPasswdStore

[attachment](/attachment)
max_size = 262144
render_unsafe_content = false

[browser](/browser)
downloadable_paths = /trunk, /branches/*, /tags/*
hide_properties = svk:merge

[changeset](/changeset)
max_diff_bytes = 10000000
max_diff_files = 0
wiki_format_messages = true

[components](/components)
trac.web.auth.LoginModule = disabled  # account manager form login requires
acct_mgr.admin.accountmanageradminpage = enabled
acct_mgr.api.accountmanager = enabled
acct_mgr.db.sessionstore = enabled
acct_mgr.htfile.abstractpasswordfilestore = enabled
acct_mgr.htfile.htdigeststore = enabled
acct_mgr.htfile.htpasswdstore = enabled
acct_mgr.notification.accountchangelistener = enabled
acct_mgr.notification.accountchangenotificationadminpanel = enabled
acct_mgr.pwhash.htdigesthashmethod = enabled
acct_mgr.pwhash.htpasswdhashmethod = enabled
acct_mgr.svnserve.svnservepasswordstore = enabled
acct_mgr.web_ui.accountmodule = enabled
acct_mgr.web_ui.loginmodule = enabled
acct_mgr.web_ui.registrationmodule = enabled
cmtekniktheme.* = enabled
codereview.peerreviewbrowser.peerreviewbrowser = disabled
codereview.peerreviewcommentcallback.userbasemodule = disabled
codereview.peerreviewinit.peerreviewinit = disabled
codereview.peerreviewmain.userbasemodule = disabled
codereview.peerreviewnew.userbasemodule = disabled
codereview.peerreviewoptions.userbasemodule = disabled
codereview.peerreviewperform.userbasemodule = disabled
codereview.peerreviewsearch.userbasemodule = disabled
codereview.peerreviewview.userbasemodule = disabled
codetags.* = enabled
forcepreview.* = enabled
forcepreview.forcepreview = disabled
includemacro.macros.includemacro = enabled
pydotorgtheme.* = enabled
themeengine.* = enabled
ticketchange.web_ui.ticketchangeplugin = enabled
ticketdelete.* = enabled
ticketdelete.web_ui.ticketdeleteplugin = enabled
traccia.cianotificationcomponent = enabled
tracdiscussion.admin.discussionwebadmin = enabled
tracdiscussion.core.discussioncore = enabled
tracdiscussion.init.discussioninit = enabled
tracdiscussion.timeline.discussiontimeline = enabled
tracdiscussion.wiki.discussionwiki = enabled
tracdownloads.admin.downloadswebadmin = enabled
tracdownloads.api.downloadsapi = disabled
tracdownloads.core.downloadscore = disabled
tracdownloads.init.downloadsinit = disabled
tracdownloads.timeline.downloadstimeline = disabled
tracdownloads.webadmin.downloadswebadmin = disabled
tracdownloads.wiki.downloadswiki = disabled
tracext.google.analytics.* = enabled
tracmetrixplugin.api.tracmetrixsetupparticipant = enabled
tracmetrixplugin.mdashboard.mdashboard = enabled
tracmetrixplugin.model.progressticketgroupstatsprovider = enabled
tracmetrixplugin.model.tickettypegroupstatsprovider = enabled
tracmetrixplugin.web_ui.milestonemetrixintegrator = enabled
tracmetrixplugin.web_ui.pdashboard = enabled
tracmetrixplugin.web_ui.roadmapmetrixintegrator = enabled
tracspamfilter.* = enabled
tracspamfilter.admin.akismetadminpageprovider = disabled
tracspamfilter.filters.akismet.akismetfilterstrategy = disabled
tractags.* = enabled
tractags.api.tagsystem = disabled
tractags.macros.listtaggedmacro = disabled
tractags.macros.tagcloudmacro = disabled
tractags.model.tagmodelprovider = disabled
tractags.ticket.tickettagprovider = disabled
tractags.web_ui.tagrequesthandler = disabled
tractags.web_ui.tagtemplateprovider = disabled
tractags.wiki.tagwikisyntaxprovider = disabled
tractags.wiki.wikitaginterface = disabled
tractags.wiki.wikitagprovider = disabled
webadmin.* = enabled

[discussion](/discussion)
title = Discussion

[downloads](/downloads)
ext = zip,gz,bz2,rar,egg
path = /var/trac/flexget/downloads
title = Downloads
unique_filename = True
visible_fields = file,description,size,time,count,version

[google.analytics](/google.analytics)
admin_logging = False
authenticated_logging = True
extensions = zip,tar,tar.gz,tar.bzip,egg
google_external_path = /external/
outbound_link_tracking = True
tracking_domain_name = flexget.com
uid = UA-729877-2

[header_logo](/header_logo)
alt = 
height = -1
link = http://flexget.com/
src = site/FlexGet2.png
width = -1

[logging](/logging)
log_file = trac.log
log_level = DEBUG
log_type = file

[mimeviewer](/mimeviewer)
enscript_modes = text/x-dylan:dylan:4
enscript_path = enscript
max_preview_size = 262144
mime_map = text/x-dylan:dylan,text/x-idl:ice,text/x-ada:ads:adb
php_path = php
silvercity_modes = 
tab_width = 8

[notification](/notification)
always_notify_owner = false
always_notify_reporter = false
always_notify_updater = true
mime_encoding = base64
smtp_always_bcc = 
smtp_always_cc = 
smtp_default_domain = 
smtp_enabled = false
smtp_from = trac@localhost
smtp_password = 
smtp_port = 25
smtp_replyto = trac@localhost
smtp_server = localhost
smtp_user = 
use_public_cc = false
use_short_addr = false
use_tls = false

[project](/project)
descr = RSS Downloader, RSS Aggregator, Downloader
footer = Visit the Trac open source project at<br /><a href="http://trac.edgewall.org/">http://trac.edgewall.org/</a>
icon = common/trac.ico
name = FlexGet
url = http://flexget.com

[search](/search)
min_query_length = 3

[spam-filter](/spam-filter)
akismet_api_key = XXXXXXX
akismet_karma = 5
extlinks_karma = 1
ip_blacklist_karma = 5
ip_throttle_karma = 3
logging_enabled = true
min_karma = 0
purge_age = 9
regex_karma = 10
session_karma = 9

[theme](/theme)
enable_css = enabled
theme = PyDotOrg

[ticket](/ticket)
default_component = flexget
default_milestone = 1.0
default_priority = major
default_type = defect
default_version = 
restrict_owner = false

[ticket-workflow](/ticket-workflow)
accept = new -> assigned
accept.operations = set_owner_to_self
accept.permissions = TICKET_MODIFY
leave = * -> *
leave.default = 1
leave.operations = leave_status
reassign = new,assigned,reopened -> new
reassign.operations = set_owner
reassign.permissions = TICKET_MODIFY
reopen = closed -> reopened
reopen.operations = del_resolution
reopen.permissions = TICKET_CREATE
resolve = new,assigned,reopened -> closed
resolve.operations = set_resolution
resolve.permissions = TICKET_MODIFY

[timeline](/timeline)
changeset_collapse_events = true
changeset_long_messages = false
changeset_show_files = 0
default_daysback = 30
ticket_show_details = true

[trac](/trac)
authz_file = 
authz_module_name = 
base_url = http://flexget.com
check_auth_ip = true
database = sqlite:db/trac.db
default_charset = iso-8859-15
default_handler = WikiModule
htdocs_location =
ignore_auth_case = false
mainnav = wiki,timeline,roadmap,browser,tickets,newticket,search
metanav = login,logout,settings,help,about
permission_store = DefaultPermissionStore
repository_dir = /home/svnroot/flexget
repository_type = svn
request_filters = None
templates_dir = /usr/share/trac/templates

[traccia](/traccia)
project_name = flexget
tickets_notifications = True
wiki_notifications = False

[wiki](/wiki)
ignore_missing_pages = false
split_page_names = false
```

**Trac directory**

```
drwxrwx--- 4 root     www-data 4096 2009-10-21 10:30 apache/
drwxrwx--- 4 root     www-data 4096 2009-10-20 22:41 attachments/
drwxrwx--- 3 root     www-data 4096 2009-10-20 22:41 cache/
drwxrwx--- 2 root     www-data 4096 2009-11-09 19:10 conf/
drwxrwx--- 2 root     www-data 4096 2009-11-09 19:24 db/
drwxrwx--- 5 root     www-data 4096 2009-10-24 19:22 downloads/
drwxrwx--- 2 root     www-data 4096 2009-10-25 21:31 htdocs/
-rw-r----- 1 root     www-data  201 2009-10-20 22:41 htpasswd.svn
-rw-rw---- 1 www-data www-data  267 2009-11-09 17:16 htpasswd.trac
drwxrwx--- 2 root     www-data 4096 2009-11-09 16:43 log/
drwxrwx--- 2 root     www-data 4096 2009-10-21 10:30 plugins/
-rw-r----- 1 root     www-data   98 2009-10-20 22:41 README
drwxrwx--- 3 root     www-data 4096 2009-10-20 22:41 templates/
-rw-r----- 1 root     www-data   27 2009-10-20 22:41 VERSION
drwxrwx--- 2 root     www-data 4096 2009-10-20 22:41 wiki-macros/
```

attachment directory is recursively 0777 and root www-data


**Debug log on adding attachment**

```
2009-11-09 18:59:41,705 Trac[main](/main) DEBUG: Dispatching <Request "POST u'/attachment/ticket/367/'">
2009-11-09 18:59:41,723 Trac[chrome](/chrome) DEBUG: Prepare chrome data for request
2009-11-09 18:59:41,755 Trac[session](/session) DEBUG: Retrieving session for ID u'username'
2009-11-09 18:59:41,762 Trac[web_ui](/web_ui) DEBUG: Not tracking TRAC_ADMIN's, returning stream
2009-11-09 18:59:41,882 Trac[main](/main) DEBUG: 472 unreachable objects found.
```