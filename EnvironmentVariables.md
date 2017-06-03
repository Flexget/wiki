# Environment Variables
Environment variables are read in certain instances by FlexGet to determine default values. Variables used by FlexGet at a "root" level, that is, those not related to a specific [plugin](/Plugin) or [CLI command](/CLI), are documented on this page. Variables which do apply to specific items are documented on the respective plugin or CLI page, links to which are in the 'Other' section below.

### Logging (Rotating logs)
| Environment Variable | Possible Values | Default Value | Description |
| --- | --- | --- | --- |
| `FLEXGET_LOG_MAXBYTES` | integer | `1024000` | Maximum bytes before creating a new file. |
| `FLEXGET_LOG_MAXCOUNT` | integer | `9` | Maximum number of log files to create before the oldest one is deleted. |

### Other Environment Variables Available in Flexget
- CLI [`series` command](/CLI/series)