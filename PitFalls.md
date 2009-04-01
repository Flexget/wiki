= Common pitfalls and answers =

=== mapping values are not allowed here, line [x] column [y] ===

 * You have : -character in somewhere where it's not allowed. If you have : in example series name, you must put name in quotes.
 * Indentation error. Thumb rule is that every time line ends with : -character next line must be indented either 2 spaces more or less. 

This is '''invalid'''

{{{
series:
  - name:
    watched:
      season: 1
}}}

It should be:

{{{
series:
  - name:
      watched:
        season: 1
}}}


=== cron job did not run - permission problems ===

Check that mta is installed(a mail system). If not, then you need to install the mail system this way as root:
{{{
aptitude install exim4 exim4-daemon-light exim4-config mutt
}}}

and configure it:

{{{
dpkg-reconfigure exim4-config
}}}
Enter mutt as the user you would like to run flexget as to see if cron is running and if eventually throws an error.
[[BR]]

Or you can install a lightweight forwarding mail service:
{{{
aptitude install ssmtp
}}}
and edit {{{/etc/ssmtp/ssmtp.conf}}} you need to set the mail server you use for outgoing mail.

If you get a mail saying {{{../flexget.py: permission denied}}} the script is not executable. You can make the script executable with chmod:
{{{
cd /path/to/flexget
chmod 0755 flexget.py
}}}

''Feel free to add more''
