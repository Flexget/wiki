= Search Plugins =

!FlexGet provides framework for querying searches from supported sites. These cannot be used directly in a task, but can be used with the [wiki:Plugins/urlrewrite_search urlrewrite_search] & [wiki:Plugins/discover discover] plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


== Overview == 

=== Public ===

||='''Keyword'''=||='''Description'''=||
||[wiki:Searches/divxatope divxatope]||Generates entries from [http://divxatope.com/ divxatope.com]||
||[wiki:Searches/flexget_archive flexget_archive]||Searches within previously archived entries||
||[wiki:Searches/isohunt isohunt]||Generates entries from [http://isohunt.com isohunt.com]||
||[wiki:Searches/kat kat]||Generate entries from [http://kat.ph kat.ph]||
||[wiki:Searches/newtorrents newtorrents]||Generates entries from [http://newtorrents.info newtorrents.info]||
||[wiki:Searches/nyaa nyaa]||Generates entries from [http://nyaa.se/ nyaa.se]||
||[wiki:Searches/piratebay piratebay]||Generates entries from [http://thepiratebay.gl/ thepiratebay]||
||[wiki:Searches/publichd publichd]||Generates entries from [http://publichd.se/ PublicHD]||
||[wiki:Searches/rarbg rarbg]||Generates entries from [http://rarbg.com/ RarBG]||
||[wiki:Searches/search_rss search_rss]||Generates query based rss feeds||
||[wiki:Searches/t411 torrent411]||Generates entries from [http://www.t411.me/ t411.me]||
||[wiki:Searches/torrentz torrentz]||Generates entries from [http://torrentz.eu torrentz.eu]||


=== Private ===

||='''Keyword'''=||='''Description'''=||
||[wiki:Searches/btn btn]||Searches torrent site BTN||
||[wiki:Searches/cpasbien cpasbien]||Generates entries from [http://www.cpasbien.pw/ cpasbien.pw]||
||[wiki:Searches/freshon freshon]||Generates entries from [http://freshon.tv freshon.tv]||
||[wiki:Searches/iptorrents iptorrents]||Generates entries from [http://iptorrents.com iptorrents.com]||
||[wiki:Searches/urlrewrite_newznab newznab]||Generates entries from [http://newznab.com newznab.com]||
||[wiki:Searches/ptn ptn]||Searches torrent site PtN||
||[wiki:Searches/morethantv morethantv]||Generates entries from [http://morethan.tv morethan.tv] (mtv)||
||[wiki:Searches/sceneaccess sceneaccess]||Searches torrent site sceneaccess||
||[wiki:Searches/torrentshack torrentshack]||Searches torrent site torrentshack||
||[wiki:Searches/torrentleech torrentleech]||Generates entries from [http://torrentleech.org/ torrentleech.org]||
||[wiki:Searches/whatcd whatcd]||Searches torrent site whatcd||

You can always get an up to date overview of the available search plugins by using the command line with command 'flexget plugins --group search', and documentation for a plugin can be obtained with 'flexget doc <plugin-name>'.

''' Example '''

{{{
flexget plugins --group search
-- Supported search plugins: --------------------------------------------------
 search_rss
 piratebay
 newzleech
 flexget_archive
 newtorrents
 torrentz
-------------------------------------------------------------------------------
}}}