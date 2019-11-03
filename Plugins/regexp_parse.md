# regexp_parse
*NOTE:* Regexp is not suitable for parsing HTML / XML reliably.

This plugin is designed to take input from a web resource or a file and parse the text via regexps supplied in the config file.

## Config settings

- **source**: is a file or url to get the data from. You can specify a username:password

- **sections**: Takes a list of dicts that contain regexps to split the data up into sections.
  The regexps listed here are used by find all so every matching string in the data will be
  a valid section.

- **keys**: hold the keys that will be set in the entries

  - **\<key name\>**:
    - **regexps**: a list of dicts that hold regexps. The key is set to the first string that matches
      any of the regexps listed. The regexps are evaluated in the order they are supplied so if a
      string matches the first regexp none of the others in the list will be used.

    - **required**: a boolean that when set to true will only allow entries that contain this key
      onto the next stage. url and title are always required no matter what you do (part of flexget)
      
- **encoding**: If the encoding of the source is not detected properly, this can be specified manually.

#TODO: consider adding a set field that will set the field to a supplied value if no matches are found

#TODO: consider a mode field that allows a growing list for a field instead of just setting to first match


## Example
```
regexp_parse:
  source: http://username:password@ezrss.it/feed/
  sections:
    - {regexp: "(?<=<item>).*?(?=</item>)", flags: "DOTALL,IGNORECASE"}

  keys:
    title:
      regexps:
        - {regexp: '(?<=<title><!\[CDATA\[).*?(?=\](/).*?(?=\)\]></title>)'} #comment
    url:
      regexps:
        - {regexp: "magnet:.*?(?=])"}
    custom_field:
      regexps:
        - {regexp: "custom regexps", flags: "comma seperated list of flags (see python regex docs)"}
      required: False
    custom_field2:
      regexps:
        - {regexp: "first custom regexps"}
        - {regexp: "can't find first regexp so try this one"}
```

TIP : You may want to use [lookaround assertions](https://www.rexegg.com/regex-lookarounds.html).
