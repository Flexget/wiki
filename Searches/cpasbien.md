= CPASBIEN Search plugin =
This search plugin will get results from [http://www.cpasbien.pe/]

== Configuration ==
Configuration requires only the category and you can only have ONE:
{{{
cpasbien: <category>
}}}

||'''Category'''||'''Description'''||
||all||Not filtered by any category||
||misc||Category for miscellaneous files||
||films||Main category for movies & other videos||
||films-french||Main category for french movies||
||1080p||Main category for 1080p movies||
||720p||Main category for 720p movies||
||films-french||Main category for french movies||
||films-dvdrip||Main category for dvdrip movies||
||films-vostfr||Main category for movies in English sub French||
||series||Category for tv shows||
||series-francaise||Category for tv shows in french||
||series-vostfr||Category for tv shows in English sub French||
||ebook||Category for books||
||musique||Category for music||

Example with discover:
{{{
          tv_search_cpasbien:
            discover:
              what:
                 - trakt_list:
                   username: xxxxxxx
                   api_key: xxxxxxx
                        series: watchlist
                  from:
                    - cpasbien:
                        category: "series-vostfr"
                  interval: 1 day
                  ignore_estimations: yes
}}}

