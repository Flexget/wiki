= Secrets =

Born to strip off passwords, api keys and other sensitive info from the configuration file, this plugin basically process some jinja2 templates on startup, to assign the corresponding values set in a dedicated yaml file.
All the templates to process must begin with the word "secrets".

=== Example ===

In this sample {{{config.yml}}} we configure the plugin to look for config secrets in a file named {{{secretfile.yml}}}:
{{{
secrets: secretfile.yml
templates:
  tell_me:
    notify_xmpp:
      sender: '{{ secrets.xmpp.usr }}'
      password: '{{ secrets.xmpp.pwd }}'
      recipient: some@recipient.xyz
      title: 'something new: {{ title }}'
tasks:
  test:
    template:
      - tell_me
    trakt_list:
      username: '{{ secrets.a_long.time_ago }}'
      password: '{{ secrets.a_long.in_a_galaxy }}'
      api_key: '{{ secrets.a_long.far.far.away }}'
      custom: test
}}}

And this is the {{{secretfile.yml}}} content:
{{{
xmpp:
  usr: xxx@yyy.zzz
  pwd: mypassword
a_long:
  time_ago: xxx
  in_a_galaxy: yyy
  far:
    far:
      away: zzz
}}}

So this will be the resulting {{{config.yml}}} before executing tasks:
{{{
secrets: secretfile.yml
templates:
  tell_me:
    notify_xmpp:
      sender: 'xxx@yyy.zzz'
      password: 'mypassword'
      recipient: some@recipient.xyz
      title: 'something new: {{ title }}'
tasks:
  test:
    template:
      - tell_me
    trakt_list:
      username: 'xxx'
      password: 'yyy'
      api_key: 'zzz'
      custom: test
}}}

'''Notes:'''
- The secrets file must stay in the same config.yml location.
- Use singles quotes around URLs in your {{{secretfile.yml}}} file.
- Any template the plugin cannot process, for any reason (i.e.: a template not starting with "secrets" or missing in the secrets file) will be ignored.
