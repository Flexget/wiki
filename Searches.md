= Search Plugins =

The [wiki:Plugins/urlrewrite_search urlrewrite_search] & [wiki:Plugins/discover discover] plugins have a set of their own private plugins. These plugins act like options for their parent plugins. This page lists these options and gives a brief description of their function.


== Overview == 

||'''Keyword'''||'''Description'''||
||[wiki:Searches/search_rss search_rss]||Generates query based rss feeds||
||[wiki:Searches/flexget_archive flexget_archive]||Searches within previously archived entries||
||[wiki:Searches/isohunt isohunt]||Generates entries from [http://isohunt.com isohunt.com]||
||[wiki:Searches/kat kat]||Generate entries from [http://kat.ph kat.ph]||
||newtorrents||Generates entries from [http://newtorrents.info newtorrents.info]||
||newzleech||broken as Newzleech.com is no more||
||[wiki:Searches/piratebay piratebay]||Generates entries from [http://thepiratebay.gl/ the piratebay]||
||[wiki:Searches/torrentleech torrentleech]||Generates entries from [http://torrentleech.org/ Torrentleech]||
||[wiki:Searches/torrentz torrentz]||Generates entries from [http://torrentz.eu Torrentz.eu]||

You can always get an up to date overview of the available search plugins by using the command line option --search-plugins

''' Example '''
{{{
flexget --search-plugins
-- Supported search plugins: --------------------------------------------------
 search_rss
 piratebay
 newzleech
 flexget_archive
 newtorrents
 torrentz
-------------------------------------------------------------------------------
}}}