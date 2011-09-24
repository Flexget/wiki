= !PyLoad =

Add url from entry url to pyload

'''Example:'''

{{{
pyload:
  api: http://localhost:8000/api
  queue: [yes|no]
  username: <user>
  password: <pwd>
  enabled: [yes|no]
}}}

Default values for the config elements:

{{{
pyload:
  api: http://localhost:8000/api
  queue: yes
  enabled: yes
}}}