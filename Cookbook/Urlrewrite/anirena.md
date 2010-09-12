= Anirena =

{{{
urlrewrite:
  aniarena:
    regexp: 'http://www.anirena.com/viewtracker.php\?action=details&id=(?P<id>\d+)'
    format: 'http://www.anirena.com/viewtracker.php?action=download&id=\g<id>'
}}}