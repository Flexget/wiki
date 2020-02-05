# SFTP Upload
Upload files to a SFTP server. 

This plugin requires the pysftp Python module; to install it module run:

```cmd
pip install pysftp
```

pysftp depends on the Pycrypto library. If you are using Windows,you may have to install it manually. Windows binaries are available [here](http://www.voidspace.org.uk/python/modules.shtml#pycrypto).

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
|  host  |  Text  |  Host to connect to  |
|  port  |  Integer  |  Port the remote SSH server is listening on. Defaults to port 22.  |
|  username  |  Text  |  Username to log in as  |
|  password  |  Text  |  The password to use. Optional if a private key is provided.  |
|  private_key  |  Path  |  Path to the private key (if any) to log into the SSH server  |
|  private_key_pass  |  Text  |  Password for the private key (if needed)  |
|  to  |  Text  |  Path to upload the file to; supports Jinja2 templating on the input entry. Fields suchas series_name must be populated prior to input into this plugin using metainfo_series or similar.  |
| delete_origin | Yes/No | Indicates wheter to delete the original file after a successful upload. |

## Example

```yaml
sftp_upload:
  host: 'hostname'
  username: 'user'
  private_key: ~/.ssh/id_rsa
  to: './TV/{{series_name}}/Season {{series_season}}/'
```
