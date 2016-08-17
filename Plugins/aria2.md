# Aria2
Passes URIs in entries to the [Aria2 downloader](http://aria2.sourceforge.net).

**Requirements:** Aria2 running and in daemon mode, with XML-RPC enabled 


| Name | Default | Required | Description |
| --- | --- | --- | --- |
| server | localhost | No | Hostname or IP of the server where Aria2 is running and has XML-RPC enabled. |
| port | 6800 | No | Port to connect to on the server listed above. |
| username | N/A | No | Username used to connect to the aria2 XML-RPC server. (Corresponds to ```rpc-user``` in the Aria2 config file.) |
| password | N/A | No | Password used to connect to the aria2 XML-RPC server. (Corresponds to ```rpc-passwd``` in the Aria2 config file.)|
| path | N/A | Yes | Output directory|
| secret | N/A | No | Aria2 `rpc-secret`|
| options | N/A | No | Any Aria2 options in key-value format.|
