= Make HTML =
Generate an HTML file for accepted entries.

Config options:

{{{file}}}: The file to create. \\
{{{template}}} (optional): Specify a custom Jinja template. Custom templates should be placed in <flexget config dir>/templates/

'''Example:'''
{{{
make_html:
  file: ~/thefile.html
}}}

'''NOTE''':
1. The Default location for templates is typically:
{{{
~/.flexget/templates
}}}
2. This directory is not created for you, and you must create the directory yourself. If you are using an alternate location then you should update the path accordingly.