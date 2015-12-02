= Search Plugins =

!FlexGet provides framework for plugins meant for querying searches from supported sites. These cannot be used directly in a task, but can be used with the [wiki:Plugins/urlrewrite_search urlrewrite_search] & [wiki:Plugins/discover discover] plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


== Overview == 

||'''Keyword'''||'''Description'''||
||[wiki:Searches/btn btn]||Searches private torrent site BTN||
||[wiki:Searches/cpasbien cpasbien]||Generates entries from [http://www.cpasbien.pw/ cpasbien.pw]||
||[wiki:Searches/flexget_archive flexget_archive]||Searches within previously archived entries||
||[wiki:Searches/freshon freshon]||Generates entries from [http://freshon.tv freshon.tv]||
||[wiki:Searches/iptorrents iptorrents]||Generates entries from [http://iptorrents.com iptorrents.com]||
||[wiki:Searches/isohunt isohunt]||Generates entries from [http://isohunt.com isohunt.com]||
||[wiki:Searches/kat kat]||Generate entries from [http://kat.ph kat.ph]||
||newtorrents||Generates entries from [http://newtorrents.info newtorrents.info]||
||newzleech||Broken as Newzleech.com is no more||
||[wiki:Searches/urlrewrite_newznab newznab]||Generates entries from [http://newznab.com newznab.com]||
||[wiki:Searches/nyaa nyaa]||Generates entries from [http://nyaa.se/ nyaa.se]||
||[wiki:Searches/piratebay piratebay]||Generates entries from [http://thepiratebay.gl/ thepiratebay]||
||[wiki:Searches/ptn ptn]||Searches private torrent site PtN||
||[wiki:Searches/publichd publichd]||Generates entries from [http://publichd.se/ PublicHD]||
||[wiki:Searches/rarbg rarbg]||Generates entries from [http://rarbg.com/ RarBG]||
||[wiki:Searches/sceneaccess sceneaccess]||Searches private torrent site sceneaccess||
||[wiki:Searches/search_rss search_rss]||Generates query based rss feeds||
||[wiki:Searches/t411 torrent411]||Generates entries from [http://www.t411.me/ t411.me]||
||torrentshack||Searches private torrent site torrentshack||
||[wiki:Searches/torrentleech torrentleech]||Generates entries from [http://torrentleech.org/ torrentleech.org]||
||[wiki:Searches/torrentz torrentz]||Generates entries from [http://torrentz.eu torrentz.eu]||
||whatcd||Searches private torrent site whatcd||


You can always get an up to date overview of the available search plugins by using the command line. On Flexget>=1.2, the command is now 'flexget plugins --group search', and documentation for a plugin can be obtained with 'flexget doc <plugin-name>'.

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