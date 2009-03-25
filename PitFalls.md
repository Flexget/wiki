= List of common pitfalls and answers to them =

'''mapping values are not allowed here'''

 * You have : -character in somewhere where it's not allowed. If you have : in example series name, you must put name in quotes.



''Feel free to add''

'''cron job did not run - permission problems'''
1. Check that mta is installed(a mail system). If not install it this way as root:
aptitude install exim4 exim4-daemon-light exim4-config mutt
and configure it:
dpkg-reconfigure exim4-config - just use the standart way
enter mutt to see what if the cron is running and an eventually error.
if it says: ~flexget/flexget.py: Permission denied
make a chmod 775 on the dir flexget

