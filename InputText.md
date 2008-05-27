= Text =

Parse any text for entries using regular expression.

{{{
url: <url>
entry:
  <field>: <regexp to match value>
format:
  <field>: <python string formatting>
}}}

Format can be used to modify matched values. All fields that were parsed are usable. You can also make temp fields for data if you need.

'''Note:''' each entry must have atleast two fields, title and url.

=== Example: ===

{{{
text:
  url: http://www.nbc.com/Heroes/js/novels.js
  entry:
    title: novelTitle = "(.*)"
    url: novelPrint = "(.*)"
  format:
    url: http://www.nbc.com%(url)s
}}}