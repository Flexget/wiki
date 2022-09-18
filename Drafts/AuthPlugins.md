---
title: AuthPlugins
description: 
published: true
date: 2022-09-18T04:57:31.445Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:28.841Z
---

# Authentication Plugins
Things I'd like to solve:
- Current authentication plugins (cookies, headers) are task wide, and can affect communication with other sites they shouldn't.
- Some plugins use their own session, and cannot currently be affected by our auth plugins.
- Enable new kinds of plugins (not strictly auth), e.g. debug plugin to print request details, request rate limiting

Config ideas for scoped auth plugins:

- Make an api v4 which passes a requests session to plugin methods. Auth plugins would have a method, `on_auth` perhaps, which would modify the session and return it. The modified session would in turn be used for all the plugins configured within the auth plugin's scope.
```
cookies:
  settings:
    file: /path/to/cookies.foo
    type: mozilla
  plugins:
    rss: http://mysite.com
    download: /somewhere
```
PRO: My favorite from an ease to implement both the framework and an auth plugin. Just modify the whole requests session, however you want. Backwards (config and plugin) compatibility: if an auth plugin is configured at task level, it would just modify task.session. CON: I don't really like my example config here, I think it's going to confuse people.
- Create a separate framework for auth plugins, with easy ways for other plugins to explicitly implement support for them.
```
rss:
  url: http://mysite.com
  auth:
    cookies:
      file: /path/to/cookies.foo
      type: mozilla
```
Then rss plugin would do something like call: `session = authframework.prepare_session(config[auth](/auth))` and use the returned session for network requests
PRO: I think the config format is maybe simplest to understand of the 3 so far. CON: Plugins must explicitly support this in their validator and create the session.
- Define auth plugins per site, rather than per plugin
```
authentication:
- site: "http://mysite.com/*"
  auth:
    headers:
      SomeHeader: Something
```
We could then customize our requests session subclass to act accordingly. PRO: If you have mixed entries from different sites, this would handle it. CON: We can't just let the auth plugins modify the session, they'd probably be limited to editing the request before being sent.
