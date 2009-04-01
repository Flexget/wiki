= List of common pitfalls and answers to them =

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
if it says: ~flexget/flexget.py: Permission denied
[[BR]]Make a chmod 775 on the dir flexget. 

''Feel free to add more''
