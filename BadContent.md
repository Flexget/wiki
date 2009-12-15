Damn spammers ...

All current spam content follows the pattern: {{{<lowercase gibberish>, <url> <one or two keywords>, <mixed case gibberish>.}}}

This regex is an attempt to match it.

{{{
[a-z]+,[ ]+http:\/\/.*?\/[ \w]+, [a-zA-Z]+\.
}}}
