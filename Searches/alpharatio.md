# Alpharatio

Search plugin for the private tracker AlphaRatio.

Config
```text
  - alpharatio:
     username: user
     password:  pass 
     scene: (yes|no) # if not set it will search both
     category: 
            tvsd,tvhd,tvdvdrip,tvpacksd,tvpackhd,moviesd,moviehd,moviepacksd,moviepackhd,
            moviexxx,mvid,gamespc,gamesxbox,gamesps3,gameswii,appspc,appsmac,appslinux,
            appsmobile,0dayxxx,ebook,audiobook,music,misc
     order_by: (seeders|leechers|time|size|year|snatched) # defaults to time
     order_desc: (yes|no) # defaults to yes
     leechstatus: (normal|freeleech|neutral leech|either) # defaults to normal
```
Multiple categories can be used.  Username and Password are required.