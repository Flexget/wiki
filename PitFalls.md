[[PageOutline]]
= Common pitfalls and answers =

== mapping values are not allowed here, line [x] column [y] ==

'''A) You have : -character in somewhere where it's not allowed.''' If you have : in example series name, you must put name in quotes.

{{{
series:
  - name
      path: ~/name/
}}}

'''Reason:''' Name is missing : at the end.


'''B) Indentation error.''' Thumb rule is that every time line ends with : -character next line must be indented either 2 spaces more or less.

This is '''invalid'''

{{{
series:
  - name:
    watched:
      season: 1
}}}

It should be:

{{{
series:
  - name:
      watched:
        season: 1
}}}

Note that you need to use an extra indentation (kind of) after a line that starts with a dash (-) and ends with a colon (:).

== !ValueError: unsupported format character '"' (0x22) at .... ==

In case you are using RSS input, try forcing it into ASCII.

{{{
rss:
  url: http://example.com
  ascii: true
}}}

== !SyntaxError: invalid syntax ==

You are trying to execute configuration file, use command:

{{{
python flexget.py
}}}

== cron job did not run - permission problems ==

Check that you have working mail system so you receive errors occur during crontab execution.

''Feel free to add more''
