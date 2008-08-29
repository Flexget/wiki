= How to file a bug report =

== How to report ==

Include as much information as possible, preferably the feed configuration and relevant log messages. You wish to remove private information from the details, please feel free to do so. Best way to do this is to replace them with *****.

When you paste configuration or log file into ticket / comment, please use `{{{...}}}` wiki-formatting. This is because otherwise all the details appear in single line. Use preview button to see that information is readable.

Example:
{{{
my config:
  rss: ******.com
  download: ~/downloads
}}}

Without `{{{...}}}` this would look like:

my config:
  rss: ******.com
  download: ~/downloads

== Additional details ==

To get more information about process you can execute !FlexGet with --debug flag, this information may be necessary to resolve the issue. When possible, please include log with --debug.
