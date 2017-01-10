# archives
Accepts entries that are valid Zip or RAR archives; reject entries that are not. This is particularly useful when notifying after extracting a multipart RAR.

This plugin requires the rarfile Python module and unrar command line utility to handle RAR
archives.

## Plugin Settings
This plugin can be enabled with a simple boolean. Alternately, if unrar isn't defined by your system's PATH environment variable, you can specify the path manually using *unrar_tool*.


| **Option** | **Decscription** |
| --- | --- |
| unrar_tool | Specifies the path of the unrar tool. Only necessary if its location is not defined in the operating system's PATH environment variable. |

## Examples
```
series-decompress:
    filesystem:
      path: /Volumes/Drobo/downloads/tv/
      recursive: yes
      regexp: '.*\.(rar|r0[01]?|zip)$'
    archives: yes
    decompress:
      keep_dirs: no
      delete_archive: no
      to: '/Volumes/Drobo/TV/{{series_name}}/Season {{series_season}}/'
      regexp: '.*\.(mkv|avi|mp4|mpg|mov|m4v)$'
```
