You can use the [wiki:Plugins/exec Exec] plugin to pass certain fields of an entry to a MySQL database. Make yourself comfortable with basic MySQL syntax first [http://dev.mysql.com/doc/refman/5.6/en/index.html here].

The correct command for [wiki:Plugins/exec Exec] on Win7 is as follows:
{{{
exec: <%SystemRoot%>\system32\cmd.exe /c <\PATH\TO\>mysql.exe -u <user> -p<pwd> --execute="INSERT INTO <table> VALUES ('{{<entry1>}}','{{<entry2>}}')" <database>
}}}
* Strings between brackets '<' and '>' represent values you need to fill in yourself: <%SystemRoot>; <\PATH\TO\>; <user>; <pwd>; <table>; <entry>; <database>
* Avoid space between your -p-trigger and your passphrase: -ppassword is correct, -p password isn't.
* You can of course extend the list of fields inserted in the database; always regard the {{{other_fields}}} option of the [wiki:Plugins/rss rss] plugin.

Please note the extended possibilities this basic tutorial in combination with other plugins.