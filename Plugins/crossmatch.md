= Crossmatch =

''TODO: write more in depth doc''

=== Reject movies rated in imdb ===

Reject movies that you have already voted on imdb. Aka old imdb_rated functionality.

{{{
crossmatch:
  from:
    - imdb_list:
        user_id: ur9999999
        list: ratings
  fields:
    - imdb_id
  action: reject
}}}

You will also need to enable [wiki:Plugins/imdb_lookup imdb_lookup] on the feed in order to get imdb_id populated. Granted, this is a lot more complicated than old imdb_rated used to be, but crossmatch allows all kinds of other clever uses as well.

=== Move movies you rated badly ===


{{{
tasks:

  sort-rated-movies:
    interval: 1 days
    history: no
    seen: no
    filesystem:
      - /path/to/collection
    imdb_lookup: yes
    crossmatch:
      from:
      - imdb_list:
          list: ratings
          login: '{{ secrets.imdb.login }}'
          password: '{{ secrets.imdb.pwd }}'
      fields:
        - imdb_id
      action: accept
    require_field:
      - imdb_score
      - imdb_user_score
    if:
      - imdb_user_score >= 7: reject
      - imdb_user_score < 7: accept
    move:
      allow_dir: yes
      to: /path/to/crap
}}}

See [wiki:Plugins/secrets secrets] plugin