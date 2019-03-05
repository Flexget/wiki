# Make HTML
Generate an HTML file for accepted entries.

Config options:

`file`: The file to create. \\
`template` (optional): Specify a custom Jinja template. Custom templates should be placed in <flexget config dir>/templates/

**Example:**
```
make_html:
  file: ~/thefile.html
```

**NOTE**:
- Custom templates should typically be placed in:
```
~/.flexget/templates
```
- This directory is not created for you. If you are using an alternate config location then you should update the path accordingly.