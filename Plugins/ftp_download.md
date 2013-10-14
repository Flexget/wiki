
== ftp_download ==
Downloads content from a ftp and saves it into a path. Path is retrieved from entry plugin receives, or if path is not set in entry, it takes the path set in the plugin config.

'''Example:'''
{{{
ftp_download:
  use-ssl: False
  use-secure: False
  skiplist: \.message|\.diz$|Sample
  path: /home/dl/tv
}}}


== Options ==

All options available are optional.

||'''Name'''||'''Description'''||
||use-ssl||Defines wether or not it should use SSL login.||
||use-secure||Defines whether or not it should use SSL/TLS downloads||
||skiplist||A regexp used to filter out unwanted paths and files.||
||path||Defines an alternative download path if none is provided in entry||

'''NOTE'''
This page describes a non-published version of the plugin.