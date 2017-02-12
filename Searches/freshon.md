# Freshon
This search plugin will get results from [http://FreshOn.tv](/http://FreshOn.tv)

## Configuration
Configuration requires username, password and passkey:
```
freshon: 
  username: xxxxxx
  password: xxxxxx
  passkey: xxxxxx
```
If you would like to define a custom category, you can use the option `category`.

 * `all` (default)
 * `webdl`
 * `hd`

If you would like only 100% or 50% freeleech, you can use the option `freeleech`.

* `all` (default)
* `free`
* `half`

Supports pagination using `page_limit` option, maximum pages is `10` (default). Number of items per page is set in the user CP at site; can only be set if you are above a certain user level. Maximum items per page is 100 meaning a total of 1000 search results maximum. 
Example:
```
freshon: 
  username: xxxxxx
  password: xxxxxx
  passkey: xxxxxx
  category: hd
  freeleech: half
```

