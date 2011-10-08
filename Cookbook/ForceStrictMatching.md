= Force Strict Matching =

''Developers thought:''[[BR]]
Not sure when this is needed, better idea would be to specify `exact` option manually for series name instead of using similar name to force FlexGet enabling it.

----

Certain time you might want to force Flexget into strict matching for a tv series. Generally Flexget will handle this quite well, but in some cases it might fail to recognise very slight differences in series names.

== An Example ==

Say a user follows a series named Seriesname, this series is broadcasted in national versions in several countries. Thus the series that exist are:

* Seriesname
* Seriesname UK

In this case Flexget for some reason is failing to understand the difference here and you are recieving episodes from both series.

== The Hack ==

To solve this we can introduce a hack into the Flexget config via [wiki:Plugins/series/regexps#Nameregexp name_regexp] to force strict matching for Seriesname

{{{
series:
  blocklist:
    - Seriesname UK:
        name_regexp: ^z{20}

}}}