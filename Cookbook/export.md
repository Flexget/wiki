Because upgrade 1.x > 2.x broke some functions, I must reset all the config directory.

So i have backup my config directory.

==== first export series TV have show ====

in the old directory we export the data
{{{
sqlite3 db-config.sqlite

.mode csv
.out series.csv
select max(season) , max(number), identifier, name from series_episodes as e join series as s where s.id = e.series_id group by e.series_id ;
.exit

awk -F "," '{ print "flexget series begin "$4 " " $3 }' series.csv >> insert_series.sh
bash insert_series.sh


}}}