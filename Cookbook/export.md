Because upgrade 1.x > 2.x broke some functions, I must reset all the config directory.

So i have backup my config directory.

==== first export series TV have show ====

Go to the old directory to export the data...

{{{
sqlite3 db-config.sqlite

sqlite> .mode csv
sqlite> .out series.csv
sqlite> select max(season) , max(number), identifier, name from series_episodes as e join series as s where s.id = e.series_id group by e.series_id ;
sqlite> .exit

awk -F "," '{ print "flexget series begin "$4 " " $3 }' series.csv >> insert_series.sh
bash insert_series.sh
}}}

==== The Seen plugin ====

Go to the old directory to export the data...

{{{
sqlite3 db-config.sqlite

sqlite> .mode insert seen_entry
sqlite> .out seen.sql
sqlite> select title,reason, feed, added, local from seen_entry ;
sqlite> .exit
}}}

Go to the new directory to import the data...

{{{
sqlite3 db-config.sqlite < ../.flexget_back/seen.sql

}}}
