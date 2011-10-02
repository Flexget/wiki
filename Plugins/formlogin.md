= Form Login =

Log in to a site using a webform

This plugin requires the mechanize library. To install it, run:

{{{
easy_install mechanize
}}}

=== Example ===

{{{
form:
  url: http://example.com/login.php
  username: <username>
  password: <password>
}}}

=== Example 2 ===

The login module just performs the login, you need to use other plugins to process content from the site:

{{{
form:
  url: http://example.com/login.php
  username: <username>
  password: <password>
html:
  url: http://example.com/browse.php?cat=1
regexp:
  accept:
    - Paddy.Obrien
}}}



== Options ==

All options except for the API key are optional

'''Options'''

||'''Name'''||'''Description'''||
||form||URL to the login form||
||username||Username to the site||
||password||Password||
||userfield||Name of the username field if not 'username'||
||passfield||Name of the password field if not 'password'||
