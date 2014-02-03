= aria2 =
Passes URIs in entries to the [http://aria2.sourceforge.net aria2 downloader].

```Requirements:``` aria2 running and in daemon mode. Daemon mode was introduced over 3 years ago, so any recent version should work.
== Configuration ==
Available configuration parameters:

||Name||Default||Mandatory||Description||
||server||localhost||No||Hostname or IP of the server where aria2 is running and has XML-RPC enabled.||
||port||6800||No||Port to connect to on the server listed above.||
||username||N/A||No||Username used to connect to the aria2 XML-RPC server. (Corresponds to ```rpc-user``` in the aria2 config file.)||
||password||N/A||No||Password used to connect to the aria2 XML-RPC server. (Corresponds to ```rpc-passwd``` in the aria2 config file.)
||do||N/A||Yes||```add-new``` or ```remove-completed```. ```add-new``` passes files to aria2 to download; ```remove-completed``` removes them (after verifying they are completed).||
||uri||N/A||Yes||The base URI to pass to aria2. Include Basic Auth parameters inline, or as their corresponding aria2 commands under aria_config below. Inline example: ```ftp://myuser:mypass@ftp.example.com:21/path/to/directory/{{title}}```. Any entry fields can be included and will be parsed prior to passing to aria2.||
||exclude_samples||No||No||Whether to exclude files containing ```sample``` in their name or parent directories.||
||exclude_non_content||Yes||No||Whether to exclude "non-content" files; that is, anything that does not have an extension listed in ```file_exts``` (see below).||
||rename_content_files||No||No||Change the names of the downloaded files. Not this does NOT change the filenames on the server or in torrents! This only changes the output files at the download location.||
||rename_template||N/A||No||If set, and rename_content_files is yes, all content files will be renamed using the value of this field as a template. It will be rendered with jinja2 and can include any fields available in the entry.||
||parse_filename||No||No||Run the filename through SeriesParser or MovieParser prior to outputting it. If you wish to use ```{{series_name}}```/```{{series_id}}``` or ```{{movie_name}}```/```{{name}}``` in your ```rename_template``` and your input plugin does not set these fields, this must be set to Yes.||
||content_is_episodes||No||No||If ```rename_content_files``` is enabled, choose whether the filenames on the server are to be parsed as episodes (meaning have a series name and series ID/episode number). If set to false, they are assumed to be movies or other non-episodic content. This must be set to Yes if you are using ```{{series_name}}``` or ```{{series_id}}``` in your ```rename_template```.||
||keep_parent_folders||No||No||If your torrent or other input has a directory structure, such as ```MyTorrentName/Sample/Sample.mkv``` and you want to keep that structure when downloading, set this to Yes.||
||fix_year||Yes||No||If the last four characters of a TV show's name are numbers, add parentheses around them in the output filename, since it is most likely a differentiating year. Only has an effect if ```parse_filename``` and ```rename_content_files``` are both enabled.||
||file_exts||see below*||No||Extensions of files to exclude as "non-content". The default is intended for video files; this could be expanded to include subtitle files, if you want those. Only has an effect if ```exclude_non_content``` or ```rename_content_files``` is enabled. Must be a comma-separated list enclosed by brackets.||
||aria_config||N/A||Yes||This is the "parent folder" of any parameters that should get passed to aria2. Any [http://aria2.sourceforge.net/manual/en/html/aria2c.html#options command line option] available in aria2 can be used by removing the two dashes (--) in front of the command name and changing ```key=value``` to ```key: value```. Any parameter can contain the name of any [http://flexget.com/wiki/Entry entry field] using [http://flexget.com/wiki/Plugins/set#Jinja2Templating jinja2 notation] and will be rendered prior to passing to aria2. See sample configuration below.||

* Default for ```file_exts```: ['.mkv', '.avi', '.mp4', '.wmv', '.asf', '.divx', '.mov', '.mpg', '.rm']

=== Sample Configuration ===
{{{
  aria2:
    server: myserver
    port: 6802
    do: add-new
    exclude_samples: yes
    exclude_non_content: yes
    parse_filename: yes
    content_is_episodes: yes
    rename_content_files: yes
    rename_template: '{{series_name}} - {{series_id||lower}}'
    aria_config:
      max-connection-per-server: 4
      max-concurrent-downloads: 4
      split: 4
      file-allocation: none
      dir: "/Volumes/all_my_tv/{{series_name}}"
}}}

In this configuration, the server and port are specified since they differ from the default. ```do``` shows we are adding new files to aria2. We want to exclude any sample videos and non-content. The filename should be parsed, and since ```content_is_episodes``` is enabled, the plugin will treat them as TV episodes. (Note the input plugin that would feed to this output is not providing any series information.)

We also want to rename the content files and provide a renaming template. Finally we are passing several commands to aria2 to affect how it processes the files, the most important of which is ```dir``` since it tells aria2 where to store the files. Note the use of [http://flexget.com/wiki/Plugins/set#Jinja2Templating jinja2 notation] to dynamically insert the  ```{{series_name}}```, per download, prior to passing to aria2. Any field in the [http://flexget.com/wiki/Entry entry] can be included in the same manner.