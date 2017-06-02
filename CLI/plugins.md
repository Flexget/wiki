---
import:
  - Includes/TableStylesDiv
---

## [CLI](/CLI) > `plugins`
Print summaries for registered [plugins](/Plugins).

### Optional arguments
| Argument | Description |
| --- | --- |
| `--group <group>`* | Show plugins belonging to specify `<group>` |
| `--phase <phase>`* | Show plugins that act on specified `<phase>` |
| `--builtins`* | Show only [builtin](/Builtin) plugins |
{{> Includes/TableStylesDiv }}

### Examples
```bash
#shows all builtin plugins
$ flexget plugins --builtins
```