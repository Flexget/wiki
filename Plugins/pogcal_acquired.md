= Pogcal Acquired =
This plugin marks the checkbox for accepted episodes on the [http://pogdesign.co.uk/cat pogdesign TV calendar].

'''Notes:'''
- This will only work for episodes that aired during the same month you download them.
- The release numbering must match up with the numbering on pogdesign for it to work. (Date and sequence type shows will not work.)
- The show name normalization probably needs some improvement to match the names on the tv calendar. Feel free to [http://flexget.com/newticket report an issue] for shows that are not working.

=== Configuration ===
This plugin takes just two options, your username and password at the pogdesign calendar.
{{{
pogcal_acquired:
  username: me@internet.com
  password: itsasecret
}}}