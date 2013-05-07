= Prowl =

Send messages to your iPhone using [http://prowlapp.com Prowl].

=== Example ===

Get your unique API key from [https://prowlapp.com/api_settings.php]

{{{
prowl:
  apikey: <your apikey>
}}}


== Options ==

All options except for the API key are optional

||'''Name'''||'''Description'''||
||apikey||Your personal API key||
||application||Application ID (default ''!FlexGet'')||
||priority||Message priority from -2 to 2. 2 = emergency ''(default 0)''||
||event||Event title shown in Prowl^*^ (default ''New release'')||
||description||Message to show^*^||
^*^ supports [wiki:Jinja jinja2] rendering from entry