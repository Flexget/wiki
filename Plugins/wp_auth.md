# WordPress Authorization
Access WordPress [s2Member](https://s2member.com/) protected RSS feeds.
## Example
```
wordpress_auth:
      url: <wordpress login-page>
      username: <wordpress username>
      password: <wordpress password>
```
## Options
Only the `url` field is required.

| Name | Description |
| --- | --- |
| `url` | The WordPress login page for the membership site (usually `wp-login.php`) |
| `username` | WordPress username |
| `password` | WordPress password |
