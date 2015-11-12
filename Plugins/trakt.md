= Trakt CLI tools =

=== auth ===

Takes two arguments, `account` and `pin`. You can generate an account specific pin by visiting http://trakt.tv/pin/346. Once you have generated this pin, you can authorize Flexget to access your Trakt.tv account by issuing the command

`flexget trakt auth <account> <pin>`. This command generates an `access_token`, which grants Flexget access to your Trakt.tv account. An `access_token` is valid for 3 months after which Flexget will automatically generate a new `access_token`.

If something should go wrong, you can issue visit http://trakt.tv/pin/346 to generate a new pin code and reissue the authorization command listed above to generate a new `access_token`.

'''We strongly recommend that you use your Trakt.tv username as `account` name to avoid confusion down the line.'''

=== refresh ===

Takes one argument `account`; the name you chose when authorizing Flexget to access your Trakt.tv account. Issuing `flexget trakt refresh <account>` will manually refresh the current `access_token` -- this command is not necessary as Flexget should automatically request a new `access_token` once it expires.

=== show ===

Takes an optional argument `account`, which shows the expiration date for the current `access_token`. If `account` is not specified, it lists all saved accounts along with their `access_token` creation dates and expiration dates.