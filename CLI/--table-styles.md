## [CLI](/CLI) > Table / list styles
Nearly all lists in the FlexGet [CLI](/CLI) support the following arguments for styling.

### Arguments
| Argument | Description |
| --- | --- |
| `--table-type {plain,porcelain,github,single,double}` | Select output table style |
  `--porcelain` | Make the output parseable. Similar to using `--table-type porcelain` |

### Examples
```bash
#use the porcelain table style
flexget series list --porcelain
#output
Name                          | Latest | Age       | Downloaded                  | Identified By
 Foo Series                   | -      | -         | -                           | ep
 Bar Series                   | S03E10 | 540d 13h  | hdtv h264                   | ep
 ...

#use the plain table style
flexget series list --table-type plain
#output
+-------------------------------+--------+-----------+-----------------------------+---------------+
| Name                          | Latest | Age       | Downloaded                  | Identified By |
+-------------------------------+--------+-----------+-----------------------------+---------------+
| Foo Series 1 behind           | S08E01 | 348d 14h  | 720p hdtv h264              | ep            |
| Bar Series                    | S03E10 | 540d 13h  | hdtv h264                   | ep            |
  ...
+-------------------------------+--------+-----------+-----------------------------+---------------+

#use the github table style
flexget series list --table-type github
#output
| Name                          | Latest | Age       | Downloaded                  | Identified By |
|-------------------------------|--------|-----------|-----------------------------|---------------|
| Banshee                       | S03E10 | 540d 13h  | hdtv h264                   | ep            |
| Castle 1 behind               | S08E01 | 348d 14h  | 720p hdtv h264              | ep            |
  ...

#use the single table style
flexget series list --table-type single
#output
lqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqwqqqqqqqqwqqqqqqqqqqqwqqqqqqqqqqqqqqqqqqqqqqqqqqqqqwqqqqqqqqqqqqqqqk
x Name                          x Latest x Age       x Downloaded                  x Identified By x
tqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqnqqqqqqqqnqqqqqqqqqqqnqqqqqqqqqqqqqqqqqqqqqqqqqqqqqnqqqqqqqqqqqqqqqu
x Foo Series                    x S03E10 x 540d 13h  x hdtv h264                   x ep            x
x Bar Series 1 behind           x S08E01 x 348d 14h  x 720p hdtv h264              x ep            x
  ...
mqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqvqqqqqqqqvqqqqqqqqqqqvqqqqqqqqqqqqqqqqqqqqqqqqqqqqqvqqqqqqqqqqqqqqqj

#use the double table style
#output
╔═══════════════════════════════╦════════╦═══════════╦═════════════════════════════╦═══════════════╗
║ Name                          ║ Latest ║ Age       ║ Downloaded                  ║ Identified By ║
╠═══════════════════════════════╬════════╬═══════════╬═════════════════════════════╬═══════════════╣
║ Foo series                    ║ S03E10 ║ 540d 13h  ║ hdtv h264                   ║ ep            ║
║ Bar series 1 behind           ║ S08E01 ║ 348d 14h  ║ 720p hdtv h264              ║ ep            ║
⋮ ...
╚═══════════════════════════════╩════════╩═══════════╩═════════════════════════════╩═══════════════╝

```