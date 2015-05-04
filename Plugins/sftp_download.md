= SFTP Download =

Download files from a SFTP server. 

This plugin requires the pysftp Python module; to install it module run:

{{{
easy_install pysftp
or
pip install  pysftp
}}}

pysftp depends on the Pycrypto library. If you are using Windows,you may have to install it manually. Windows binaries are available [http://www.voidspace.org.uk/python/modules.shtml#pycrypto here].

== Example ==

{{{
sftp_download:
  to: '/Volumes/External/Drobo/downloads'
  delete_origin: False
}}}

== Options ==

||'''Name'''||'''Info'''||'''Description'''||
|| to || Path || Destination path; supports Jinja2 templating on the input entry. Fields such as series_name must be populated prior to input into this plugin using metainfo_series or similar. ||
|| recursive || [Yes|No] || Indicates wether to download directory contents recursively. ||
|| delete_origin || [Yes|No] || Indicates wether to delete the remote files(s) once they've been downloaded. ||