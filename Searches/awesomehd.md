# AwesomeHD
This search plugin will get tv/movie results from AwesomeHD. While their API provides a `type` parameter in the response, it seems to always be `Movie`.

## Configuration
Only required parameter is `passkey`, which can be found on your AHD profile. This key is unique to your account so guard it well!
```
awesomehd:
  passkey: <passkey>
  only_internal: true|false (default false)
```