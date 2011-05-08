= !MyEpisodes =

Marks a series episode as acquired in your myepisodes.com account.

'''Simple Example'''

Most shows are recognized automatically from their TVDBname. And of course the plugin needs to know your !MyEpisodes account details.
{{{
feeds:
  tvshows:
    myepisodes:
      username: <username>
      password: <password>
    series:
      - human target
      - chuck
}}}

'''Advanced Example'''

In some cases, the TVDB name is either not unique or won't even be discovered. In that case you need to specify the !MyEpisodes id manually using the set plugin.
{{{
feeds:
  tvshows:
    myepisodes:
      username: <username>
      password: <password>
    series:
      - human target:
        set:
          myepisodes_id: 5111 
      - chuck
}}}
 
Have a look at the attached image for how to find the correct series ID on the !MyEpisodes homepage. 