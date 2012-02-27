= Proxy =
Configures !FlexGet to use a proxy when accessing sites. This plugin will be automatically configured if you have the appropriate environment variables set. (http_proxy, https_proxy or ftp_proxy)

'''NOTE:''' Not all communication will go through the proxy, only certain plugins have been refactored to use this. The [wiki:Plugins/rss rss] and [wiki:Plugins/download download] plugins will both use this proxy.

'''Example:'''
{{{
proxy: http://myproxy.com:8080
}}}

'''Example:'''

If you need to configure a proxy for only one protocol, or different proxies for different protocols, this configuration style can be used.
{{{
proxy:
  http: http://myproxy.com:8080
  ftp: http://otherproxy.com:9090
}}}