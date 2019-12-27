# Input CSV
Adds support for CSV format (comma-delimited only). Configuration may seem a bit complex,
but this has advantage of being universal solution regardless of CSV
and internal entry fields.

Configuration format:

```yaml
csv:
  url: <url>
  values:
    <field>: <number>
```

Example DB-fansubs:

```yaml
csv:
  url: http://www.dattebayo.com/t/dump
  values:
    title: 3  # title is in 3rd field
    url: 1    # download url is in 1st field
```

Example with local file:

```yaml
csv:
      url: file:///home/pi/flexget/output.csv
      values:
        filename: 1
        title: 2
        url: 3
```

Fields title and url are mandatory. First field is 1.
List of other common (optional) fields can be found from [entries](/Entry) documentation.