= Authentication Plugins =

Things I'd like to solve:
- Current authentication plugins (cookies, headers) are task wide, and can affect communication with other sites they shouldn't.
- Some plugins use their own session, and cannot currently be affected by our auth plugins.
- Enable new kinds of plugins, e.g. debug plugin to print request details, request rate limiting

Config ideas for scoped auth plugins:

- Make an api v4 which passes a requests session to plugin methods. Auth plugins would have a method, `on_auth` perhaps, which would modify the session and return it. The modified session would in turn be used for all the plugins configured within the auth plugin's scope.
{{{
cookies:
  settings:
    file: /path/to/cookies.foo
    type: mozilla
  plugins:
    rss: http://mysite.com
    download: /somewhere
}}}
- Create a separate framework for auth plugins, with easy ways for other plugins to explicitly implement support for them.
{{{
rss:
  url: http://mysite.com
  auth:
    cookies:
      file: /path/to/cookies.foo
      type: mozilla
}}}
Then rss plugin would do something like call: `session = authframework.prepare_session(config['auth'])` and use the returned session for network requests
