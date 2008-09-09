= CookBook = 

Feel free to add your own recipes.

== Index ==

 * [wiki:CookBook#DownloadFlexGetReleases Download FlexGet releases]
 * [wiki:CookBook#DownloadHeroesComis Download Heroes Comics]

== Download !FlexGet Releases ==

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


== Download Heroes Comics ==

Download all/new heroes comics from [http://nbc.com/Heroes nbc.com]

{{{
heroes:
  text:
    url: http://www.nbc.com/Heroes/js/novels.js
    entry:
      title: novelTitle = "(.*)"
      url: novelPrint = "(.*)"
    format:
      url: http://www.nbc.com%(url)s
  download: ~/heroes/

}}}