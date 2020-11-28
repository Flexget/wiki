# Proxy
Configures FlexGet to use a proxy when accessing sites. This plugin will be automatically configured if you have the appropriate environment variables set. (http_proxy, https_proxy or ftp_proxy)

**NOTE:** Not all communication will go through the proxy, only certain plugins have been refactored to use this. The [rss](/Plugins/rss) and [download](/Plugins/download) plugins will both use this proxy.

**Example:**
```
proxy: http://myproxy.com:8080
```

**Example:**

If you need to configure a proxy for only one protocol, or different proxies for different protocols, this configuration style can be used.
```
proxy:
  http: http://myproxy.com:8080
  ftp: http://otherproxy.com:
  socks5: socks5://proxy:22
```

**NOTE:** The proxy plugin requires pysocks as a dependency. In order to use the proxy plugin, it may be necessary to install the pysocks package: `pip install pysocks`