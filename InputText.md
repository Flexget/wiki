= Text =

Parse any text for entries using regular expression.

{{{
text:
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
  # construct our entry with this data
  entry:
    title: novelTitle = "(.*)"
    url: novelPrint = "(.*)"
  # further format entry
  format:
    url: http://www.nbc.com%(url)s
}}}