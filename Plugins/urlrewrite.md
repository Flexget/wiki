= URL Rewrite =

''TODO: write ... ''

{{{
urlrewrite:
  imaginary:
    regexp: 'http://imaginary.org/tor/(?P<id>\d+)/(?P<name).*)'
    format: 'http://imaginary.org/download/\g<id>/\g<name>'
}}}

This would rewrite url

{{{
http://imaginary.org/tor/1234/test.torrent
}}}

to:

{{{
http://imaginary.org/download/1234/test.torrent
}}}
