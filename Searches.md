= Search Plugins =

The [wiki:Plugins/urlrewrite_search urlrewrite_search] & [wiki:Plugins/discover discover] plugins have a set of their own private plugins. These plugins act like options for their parent plugins. This page lists these options and gives a brief description of their function.


== Overview == 

||'''Keyword'''||'''Description'''||
||[wiki:Searches/search_rss search_rss]||Generates query based rss feeds||
||[wiki:Searches/demonoid demonoid]||Generates entries from [http://demonoid.me demonoid.me]||
||[wiki:Searches/flexget_archive flexget_archive]||Searches within previously archived entries||
||[wiki:Searches/isohunt isohunt]||Generates entries from [http://isohunt.com isohunt.com]||
||newtorrents||Generates entries from [http://newtorrents.info newtorrents.info]||
||newzleech||broken as Newzleech.com is no more||
||nzbmatrix||Generates entries from [http://nzbmatrix.com Nzbmatrix.com]||
||piratebay||Generates entries from [http://thepiratebay.org/ the piratebay]||
||torrentz||Generates entries from [http://torrentz.eu Torrentz.eu]||

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
 
 nzbmatrix
-------------------------------------------------------------------------------
}}}