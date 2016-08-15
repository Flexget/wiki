# Make HTML
Generate an HTML file for accepted entries.

### Configuration

|Option|Description|
|---|---|
|file| The file to create.|
|template| Optionally specify a custom [Jinja2](/Jinja) template. Custom templates should be placed in `<config dir>/templates/`. This directory is not created automatically for you.|

#### Example

```yaml
make_html:
  file: ~/thefile.html
```

```yaml
make_html:
  file: ~/thefile.html
  template: foobar.html
```

