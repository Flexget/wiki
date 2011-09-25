= pyLoad =

Adds url from entries to pyload

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

== Prerequisites ==
Make sure [http://pyload.org pyLoad] is running and you have at least version '''0.4.8'''. The webinterface needs to be activated and accessible, so FlexGet can use the API.

The '''api''' parameter should be the address of the webinterface followed by "/api", in case the webinterface runs locally on port 8000 the default value will be ok.
Don't forget to set correct '''username''' and '''password'''.

If '''queue''' is activated downloads will start immediately, otherwise go to collector.

