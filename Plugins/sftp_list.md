# SFTP List
Generate entries from SFTP to download with [sftp_download](sftp_download). This plugin requires the pysftp Python module and its dependencies.

This plugin requires the pysftp Python module; to install it run:

```
pip install  pysftp
```
**NOTE:** If experiencing issues with connections, you may need to [downgrade](https://github.com/Yenthe666/auto_backup/issues/47) pysftp to 0.2.8 (if using 0.2.9).

This can easily be done by running:
```
pip uninstall pysftp
pip install pysftp==0.2.8
```
pysftp depends on the Pycrypto library. If you are using Windows, you may have to install it manually. Windows binaries are available [here](http://www.voidspace.org.uk/python/modules.shtml#pycrypto).

**NOTE:** If experiencing issues with connections, you may need to [downgrade](https://github.com/Yenthe666/auto_backup/issues/47) pysftp to 0.2.8 (if using 0.2.9).

This can easily be done by running:
```
pip uninstall pysftp
pip install pysftp==0.2.8
```

**Example**

```
sftp_list:
  host: example.com
  username: Username
  private_key: /Users/username/.ssh/id_rsa
  recursive: False
  get_size: True
  files_only: False
  dirs: 
    - '/path/to/list/'
    - '/another/path/'
```

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
|  host  |  Text  |  Host to connect to  |
|  port  |  Number |  Port the remote SSH server is listening on. Defaults to port 22.  |
|  username  |  Text  |  Username to log in as  |
|  password  |  Text  |  The password to use. Optional if a private key is provided.  |
|  private_key  |  Path  |  Path to the private key (if any) to log into the SSH server  |
|  private_key_pass  |  Text  |  Password for the private key (if needed)  |
|  recursive  |  [Yes\|No]  |  Indicates whether the listing should be recursive  |
|  get_size  |  [Yes\|No]  |  Indicates whether to calculate the size of the remote file/directory. WARNING: This can be very slow when computing the size of directories!  |
|  files_only  |  [Yes\|No]  |  Indicates whether to omit directories from the results.  |
| dirs | Text | List of directories to list |