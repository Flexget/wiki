= CookBook = 

Feel free to add your own recipes.

== Index ==

 * [wiki:CookBook#DownloadFlexGetreleases Download !FlexGet releases]



== Download !FlexGet releases ==

{{{
flexget:
  html: http://download.flexget.com
  patterns:
    - flexget_\(r\d*\)
  download: ~/flexget/
  interval: 3 days
}}}

Execute !FlexGet once with parameters:

{{{
flexget.py --feed flexget --learn
}}}

This will learn all matches as already downloaded, thus avoids downloading old versions.