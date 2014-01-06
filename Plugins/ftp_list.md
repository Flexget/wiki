
== ftp_list ==
Generate entries from a remote FTP server

'''Configuration:'''
{{{
ftp_list:
  config:
    use-ssl: no
    name: <ftp name>
    username: <username>
    password: <password>
    host: <host to connect>
    port: <port>
  dirs:
    - <directory 1>
    - <directory 2>
    - ....
}}}