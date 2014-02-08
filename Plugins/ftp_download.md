== ftp_download ==
Downloads content from a ftp and saves it into a local path. Path is retrieved from an entry plugin. The Entry URL must contain the FTP username and password

'''{{{NOTE:}}}''' The `ftp_tmp_path` option will probably be changed to just `path` for consistency with other plugins. #2443

'''Example:'''
{{{
ftp_download:
  use-ssl: False
  delete_origin: False
  ftp_tmp_path: /home/dl/tv
}}}


== Options ==

All options available are optional.

||'''Name'''||'''Description'''||
||use-ssl||Defines wether or not it should use SSL login.||
||ftp_tmp_path||Defines the local path in which the medias will be downloaded.||
||delete_origin||If set to True (False by default), the downloaded content will be deleted on the server after successful retrieval||
