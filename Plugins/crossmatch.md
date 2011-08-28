= Crossmatch =

''TODO: write more in depth doc''

'''Example:'''

Reject movies that you have already voted on imdb. Aka old imdb_rated functionality.

{{{
crossmatch:
  from:
    - imdb_list:
        username: username
        password: password
        list: ratings
  fields:
    - imdb_id
  action: reject
}}}

You will also need to enable [wiki:Plugins/imdb_lookup imdb_lookup] on the feed in order to get imdb_id populated. Granted, this is a lot more complicated than old imdb_rated used to be, but crossmatch allows all kinds of other clever uses as well.