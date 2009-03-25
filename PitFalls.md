= List of common pitfalls and answers to them =

'''mapping values are not allowed here'''

 * You have : -character in somewhere where it's not allowed. If you have : in example series name, you must put name in quotes.



''Feel free to add''

'''cron job did not run - permission problems'''
[[BR]]Check that mta is installed(a mail system). If not, then you need to install the mail system this way as root:
[[BR]]aptitude install exim4 exim4-daemon-light exim4-config mutt
and configure it:
[[BR]]dpkg-reconfigure exim4-config - just use the standart way
[[BR]]Enter mutt as the user you would like to run flexget as to see if cron is running and if eventually throws an error.
if it says: ~flexget/flexget.py: Permission denied
[[BR]]Make a chmod 775 on the dir flexget. 

