= Form Login =

Log in to a site using a webform

=== Example ===

{{{
form:
  url: http://example.com/login.php
  username: <username>
  password: <password>
}}}

=== Example 2 ===

The login module just performs the login, you need to use other modules to parse entries from the site:

{{{
form:
  url: http://example.com/browse.php
  username: <username>
  password: <password>
html:
  url: http://example.com/browse.php?cat=1
regexp:
  accept:
    - Paddy.Obrien
}}}