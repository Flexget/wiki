= Prowl =

Send messages to your iPhone using [http://prowl.weks.net/ Prowl].

=== Example ===

Get your unique API key from [https://prowl.weks.net/settings.php]

{{{
prowl:
  apikey: <your apikey>
}}}


== Options ==

All options except for the API key are optional

'''Options'''

||'''Name'''||'''Description'''||
||apikey||Your personal API key||
||event||Event title shown in Prowl (default ''New release'')||
||priority||Message priority from -2 to 2. 2 = emergency ''(default 0)''||
