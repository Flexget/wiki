
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
||path||Defines the local path in which the medias will be downloaded.||
||delete_origin||If set to True (False by default), the downloaded content will be deleted on the server after successful retrieval||
