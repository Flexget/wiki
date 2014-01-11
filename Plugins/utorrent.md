= uTorrent =
This plugin passes entry URLs directly to uTorrent to be added. Supports dynamically setting the save path. You must set up your allowed download directories for the uTorrent webui to contain a parent folder of any path you wish to be able to save to from !FlexGet.

'''Note:''' This plugin can currently only pass the URL to uTorrent, which means that any custom authentication plugins (cookies, headers, etc.) will not apply. A pull request to fix this would be welcomed. :-)

=== Example ===
{{{
utorrent:
  url: http://localhost:8080/gui/
  username: my_username
  password: my_password
  path: c:\stuff\here  # Either c:\stuff, or c:\stuff\here must be added to your allowed download folders for this example path to work.
}}}