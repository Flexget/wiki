
== ftp_list ==
Generate entries from a remote FTP server

'''Configuration:'''
{{{
ftp_list:
  config:
    name: <ftp name>
    username: <username>
    password: <password>
    host: <host to connect>
    port: <port>
    [use-ssl: no]
    [encoding: auto]
  dirs:
    - <directory 1>
    - <directory 2>
    - ....
}}}