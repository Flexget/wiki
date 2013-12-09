
== ftp_download ==
Downloads content from a ftp and saves it into a local path. Path is retrieved from an entry plugin. The Entry URL must contain the FTP username and password

'''Example:'''
{{{
ftp_download:
  use-ssl: False
  delete_origin: False
  path: /home/dl/tv
}}}


== Options ==

All options available are optional.

||'''Name'''||'''Description'''||
||use-ssl||Defines wether or not it should use SSL login.||
||use-secure||Defines whether or not it should use SSL/TLS for downloads.||
||skiplist||A regexp used to filter out unwanted paths and files.||
||path||Defines an alternative download path if none is provided in entry.||

'''NOTE'''
This page describes a non-published version of the plugin.