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