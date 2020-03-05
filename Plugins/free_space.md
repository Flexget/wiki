# Free Space
This plugin will abort a task if free space on a given drive is getting low.


| **Option** |     **Values** | **Description** |
| --- | ------- | --- |
| path | \<directory path> | The path to monitor for free space. |
| space | \<integer> | Amount of free space (in MB) that you require for new entries to be allowed. |
| port <sup>**a**</sup> | \<integer> | The port used for SSH connection to remote server. Default is 22. |
| host <sup>**b**</sup> | \<URL/IP>| The URL or IP address of the remote server. Often similar to `unique.hostingcompany.com`.|
| user <sup>**b**</sup> | \<username> | The username that is used to login to the remote server.|
| ssh_key_filepath <sup>**b**</sup> | \<directory path> | The directory path to the public RSA key. This is needed for passwordless login. Often `/home/user_name/.ssh/id_rsa`. [Example setup guide](https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/).|
| allotment <sup>**c**</sup> | \<integer> | The amount of space that is allowed to be used (in MB) on the remote server. |

**a/b/c:** These options are only used if checking for free space on a remote server.

**a:** Only use this option if the remote server is listening for an SSH connection on a port that is different than port 22.

**b:** These three options are required for checking for free space on a remote server.

**c:** Only use this option if the remote server that is being accessed has shared disk space with other users. When using this option, make sure that the 'path' option is set to your remote 'home' directory.

### Examples:

**Basic example**:

Abort task if less than 500MB remaining on the disk where `/location/to/monitor` is located.

```
free_space:
  path: location/to/monitor
  space: 500
```
**Basic remote server example**:

Abort task if less than 5000MB (5GB) remaining on the disk where `/remote/location/to/monitor` is located. Remote paths must be enclosed in quotation marks. 

```
free_space:
  path: '/remote/location/to/monitor'
  space: 5000
  host: 'unique.hostingcompany.com'
  user: 'remote_username'
  ssh_key_filepath: /home/local_username/.ssh/id_rsa
```

**Advanced remote server example**:

Abort task if less than 15000MB (15GB) remaining in the directory where `/media/sdh1/username` is located. This assumes that 1000000MB (1TB) of usage is allowed and the user's home directory is specified by `path`. This also assumes that the remote server is listening on port 8022 for an SSH connection. Remote paths must be enclosed in quotation marks. 

```
free_space:
  port: 8022
  path: '/media/sdh1/username'
  space: 15000
  host: 'unique.hostingcompany.com'
  user: 'remote_username'
  ssh_key_filepath: /home/local_username/.ssh/id_rsa
  allotment: 1000000
```
