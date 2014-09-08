This is my current flexget configuration. I think mine is a little different than most because I'm not on a linux machine. I think most people use transmission to manage their torrent downloads. I didn't have much luck getting transmission-qt to work. What I do instead is to save the torrents to a blackhole and use a script to pass them to aria2. I'll post the script once I finish debugging. 

Also, I haven't seen anyone else use both torrent files and magnet links. Below is a technique that will download the torrent file if available or create a file containing the magnet link for future parsing.

{{{
schedules:
  - tasks: 'WWE-Raw'
    interval:
      hours: 12
  - tasks: 'tv'
    interval:
      minutes: 5

templates:
  tv-common:
    inputs:
      - rss: http://kat.ph/tv/?rss=1      
      - rss: http://showrss.info/feeds/all.rss
      - rss: http://rss.thepiratebay.se/208
  wrestling-common:
    headers:
      Cookie: "uid=*********; pass=******"   
    download: yes
    set:
      path: D:/Blackhole/Torrents/WWE/

tasks:
  WWE-Raw:
    rss: 
      url: http://xtremewrestlingtorrents.net/rss.php?*****
      title: title
    template: wrestling-common
    regexp:
      reject:
        - german
    series:
      - Monday Night Raw:
          quality: 720p
          name_regexp:
            - Monday\.Night\.Raw
      - Friday Night Smackdown:
          quality: "<=720p"
          name_regexp:
            - Friday\.Night\.Smackdown
      - Main Event:
          quality: "<=720p"
          name_regexp:
            - Main\.Event
      - NXT:
          quality: "<=720p"
  tv:
    template: tv-common
    pushover:
        userkey: 
            - ******
        apikey: ******
        device: lg-ls720
        title: Snatched {{series_name}}
        message: Episode {{series_id}}
    if:      
      - "'magnet' not in url.lower()":
          download: yes
      - "'magnet' in url.lower()":
          exec: 'echo "{{url}}" > "D:/Blackhole/Torrents/TV/{{title}}.magnet"'
    set:
      path:  D:/Blackhole/Torrents/TV/
    torrent_alive: yes
    regexp:
      reject:
        - \WSubs\W
    series:
      720p:
        - A Haunting
        - Amish Haunting
        - Anger Management
        - Aqua TV Show Show
        - Archer
        - The Big Bang Theory
        - Black Jesus
        - The Blacklist
        - Boardwalk Empire
        - Bob's Burgers
        - The Boondocks
        - Brickleberry
        - The Bridge
        - Castle
        - Celebrity Ghost Stories
        - The Cleveland Show
        - Community
        - Continuum
        - The Daily Show
        - Defiance
        - Destination Truth
        - Doctor Who
        - Dominion
        - Downton Abbey
        - Elementary
        - Episodes
        - Falling Skies
        - Family Guy
        - Fargo
        - Fringe
        - Game of Thrones
        - Ghost Asylum
        - Grimm
        - Haven
        - Helix
        - Intruders
        - Key & Peele
        - The Last Ship
        - Long Island Medium
        - The Mentalist
        - Motive
        - MythBusters
        - Nathan for You
        - Once Upon a Time
        - Orphan Black
        - Parks and Recreation
        - Penny Dreadful
        - Person of Interest
        - Portlandia
        - Review
        - Robot Chicken
        - Salem
        - Saturday Night Live
        - Sherlock
        - Silicon Valley
        - The Simpsons
        - Sirens
        - The Soup
        - South Park
        - The Strain
        - Top Gear
        - Tosh 0
        - Total Divas
        - True Detective
        - Under the Dome
        - Utopia:
            name_regexp:
              - ^(?!AU)
        - The Vampire Diaries
        - Veep
        - Wipeout

}}}