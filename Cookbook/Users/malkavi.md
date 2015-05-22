After reading other users config and Flexget code, I have write my own config and prepare some PR to search movies in Spanish webs.

I have split my config in several files and include in the main config

NewPCT1
{{{
rss:
  url: http://www.newpct1.com/feed
  link: link
series:
  settings:
    normales:
      quality: hdtv <720p
      ep_regexp:
        - Cap.(\d+)(\d\d)
  normales:
    - Arrow
    - Juego de Tronos
    - Vikingos
    - Powers
regexp:
  reject:
    - V.O.:
        from: title
download:
  path: /home/osmc/torrents/
}}}
