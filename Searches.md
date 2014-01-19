= Search Plugins =

!FlexGet provides framework for plugins meant for querying searches from supported sites. These can be used with the [wiki:Plugins/urlrewrite_search urlrewrite_search] & [wiki:Plugins/discover discover] plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


== Overview == 

||'''Keyword'''||'''Description'''||
||[wiki:Searches/btn btn]||Searches private torrent site BTN||
||[wiki:Searches/flexget_archive flexget_archive]||Searches within previously archived entries||
||[wiki:Searches/isohunt isohunt]||Generates entries from [http://isohunt.com isohunt.com]||
||[wiki:Searches/kat kat]||Generate entries from [http://kat.ph kat.ph]||
||newtorrents||Generates entries from [http://newtorrents.info newtorrents.info]||
||newzleech||broken as Newzleech.com is no more||
||[wiki:Searches/piratebay piratebay]||Generates entries from [http://thepiratebay.gl/ the piratebay]||
||[wiki:Searches/publichd publichd]||Generates entries from [http://publichd.se/ PublicHD]||
||[wiki:Searches/search_rss search_rss]||Generates query based rss feeds||
||[wiki:Searches/torrentleech torrentleech]||Generates entries from [http://torrentleech.org/ Torrentleech]||
||[wiki:Searches/torrentz torrentz]||Generates entries from [http://torrentz.eu Torrentz.eu]||
||[wiki:Searches/urlrewrite_newznab urlrewrite_newznab]||Search a newznab website for entries.||

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