# Third-Party and Extra Plugins
These are plugins that are made by third parties, not common, actively maintained or are otherwise unsuitable for main distribution.

### Adding Your Plugin
If you wish to add your plugin to this list, please edit this page and add a new row in the "Third-Party Plugins" table. The template and instructions for a plugin wiki page is found [here](/Site/ThirdPartyPluginTemplate).

Your plugin's wiki page must be located under `/Plugins` on this site, unless it is a search plugin, in which case it belongs under `/Searches`. For example, `/Plugins/my_plugin_name` or `/Searches/my_plugin_name`. `my_plugin_name` must correspond to your plugin's name as it is used in the config file. Visiting https://flexget.com/Plugins/\<my_plugin_name> will result in an editor screen that allows you to add the new wiki page.

### Third-Party Plugins
Refer to the wiki page for download link and installation instructions.
| **Name** | **Description** |
| --- | --- | --- |
| [`app_deluge_find`](/Plugins/app_deluge_find) | Plugin specifically for macOS which provides compatibility with Deluge.app (instead of requiring installation of the deluge package). |

### FlexGet Extras Package

These plugins are not included in the core package and must be installed from the FlexGet [GitHub repository](https://github.com/Flexget/extras).

| **Name** | **Description** |
| --- | --- |
| [`uoccin_emit`](/Plugins/uoccin_emit) | Produce entries from a [Uoccin](https://github.com/tarzasai/Uoccin) data file |
| [`uoccin_collection_add`](/Plugins/uoccin_collection) | Mark all the accepted movies/episodes as collected in the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_collection_remove`](/Plugins/uoccin_collection) | Unmark all the accepted movies/episodes as collected in the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_watched_true`](/Plugins/uoccin_watched) | Mark all the accepted movies/episodes as watched in the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_watched_false`](/Plugins/uoccin_watched) | Unmark all the accepted movies/episodes as watched in the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_watchlist_add`](/Plugins/uoccin_watchlist) | Add all the accepted movies/series in the watchlist inside the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_watchlist_remove`](/Plugins/uoccin_watchlist) | Remove all the accepted movies/series from the watchlist inside the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_subtitles`](/Plugins/uoccin_subtitles) | Update the list of subtitles downloaded for the accepted movies/series in the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_lookup`](/Plugins/uoccin_lookup) | Fetch all the supported information from the [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
| [`uoccin_reader`](/Plugins/uoccin_reader) | Synchronize a [Uoccin](https://github.com/tarzasai/Uoccin) data file. |
