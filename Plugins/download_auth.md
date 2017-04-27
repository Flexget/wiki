# Download Authentication

In case accepted files that are passed to download plugin require basic or digest authentication, you can set it using this plugin.

## Configuration:
```yaml
download_auth:
- [STRING_TO_MATCH_IN_URL]:
    username: USERNAME
    passsword: PASSWORD
    type: basic|digest (default is basic)
```

## Example:
```yaml
tasks:
  auth_test:
    mock:
    - title: bla
      url: https://httpbin.org/digest-auth/auth/user/passwd/MD5
    download_auth:
    - https://httpbin.org:
        username: user
        password: passd
        type: digest
    accept_all: yes
    download: ~/
```
Note that key name can be any valid regexp, for example:
```yaml
download_auth:
- "http?s://sitename.(com|net)":
     username: foo
     password: bazz
```