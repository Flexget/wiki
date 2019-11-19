# Alpharatio

Search plugin for the private tracker AlphaRatio.

Config
```text
  - alpharatio:
     username: user
     password:  pass 
     scene: (yes|no) # if not set it will search both
     category: 
            tvsd, tvhd, tvuhd, tvdvdrip, tvpacksd, tvpackhd, tvpackuhd, moviesd, moviehd, movieuhd, moviepacksd, 
            moviepackhd, moviepackuhd, moviexxx, bluray, animesd, animehd, gamespc, gamesxbox, gamesps, gamesnin, 
            appswindows, appsmac, appslinux, appsmobile, 0dayXXX, ebook, audiobook, music, misc
     order_by: (seeders|leechers|time|size|year|snatched) # defaults to time
     order_desc: (yes|no) # defaults to yes
     leechstatus: (normal|freeleech|neutral leech|either) # defaults to normal
```
Multiple categories can be used.  Username and Password are required.