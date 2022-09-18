---
title: 404notfound
description: 
published: true
date: 2022-09-18T05:22:27.690Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:25.076Z
---

This is my current flexget configuration. I think mine is a little different than most because I'm not on a linux machine. I think most people use transmission to manage their torrent downloads. I didn't have much luck getting transmission-qt to work. What I do instead is to save the torrents to a blackhole and use a script to pass them to aria2. I'll post the script once I finish debugging. 

Also, I haven't seen anyone else use both torrent files and magnet links. Below is a technique that will download the torrent file if available or create a file containing the magnet link for future parsing.

*** Update *** 

Added section to download comic book series. Still torn between using series or just downloading everything or using a regexp to match titles. The series plugin works pretty good so far for this purpose.

```
schedules:
  - tasks: 'WWE-Raw'
    interval:
      days: 1
      at_time: 3:30 am
  - tasks: 'Comics'
    interval:
      minutes: 5
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
      Cookie: "uid=757956; pass=f12a628f6b0673b4b62e40e343c37e69"   
    download: yes
    set:
      path: D:/Blackhole/Torrents/WWE/

tasks:
  Comics:
    inputs:
      - rss: http://kickass.to/comics/?rss=1
      - rss: http://rss.thepiratebay.se/602
      - rss: http://kickass.to/usearch/category%3Acomics%20seeds%3A100%20age%3Amonth/?rss=1
      - rss: http://kickass.to/usearch/category%3Acomics%20user%3ANemesis43%20seeds%3A100/?rss=1
    set:
      path:  D:/Blackhole/Torrents/Comics/    
    if:      
      - "'magnet' not in url.lower()":
          download: yes
      - "'magnet' in url.lower()":
          exec: 'echo "{{url}}" > "D:/Blackhole/Torrents/Comics/{{title}}.magnet"'
    torrent_alive: yes    
    manipulate:
      - title:
          replace:
            regexp: 'annual (\d){1,4}'
            format: 'Special A\1'
      - title:
          replace:
            regexp: 'special (\d){1,3}'
            format: 'Special SP\1'
    series:
      settings:
        default:
          identified_by: sequence
      default:
        # DC
        - Action Comics Futures End # One-Shot
        - Aquaman Futures End # One-Shot
        - Astro City
        - Batgirl Futures End # One-Shot?
        - Batman Futures End # One-Shot?
        - Batman Eternal:
            begin: 22
        - Batwing Futures End # One-Shot
        - Birds Of Prey Futures End # One-Shot?
        - Coffin Hill
        - Constantine Futures End # One-Shot?
        - Detective Comics Futures End # One-Shot
        - Earth 2 Futures End # One-Shot
        - Fairest:
            begin: 29
        - Grayson Futures End # One-Shot
        - Green Arrow Futures End # One-Shot
        - Green Lantern Corps Futures End # One-Shot
        - Green Lantern Futures End # One-Shot
        - Hinterkind:
            begin: 11
        - Infinity Man And The Forever People Futures End # One-Shot?
        - Injustice Gods Among Us Year Two
        - Justice League:
            begin: 33
        - Justice League United Futures End # One-Shot
        - Legends Of The Dark Knight 100-Page Super-Spectacular
        - Names # Limited Series 1-8
        - New 52 Futures End:
            begin: 18
        - New Suicide Squad Futures End # One-Shot
        - Superboy Futures End # One-Shot
        - Superman Unchained:
            begin: 8 
        - Swamp Thing Futures End # One-Shot
        - Trinity Of Sin The Phantom Stranger Futures End # One-Shot
        - Worlds' Finest Futures End # One-Shot

        - 100 Bullets
        - Daredevil
        - Batman:
            exact: yes
        - Batman and Robin:
            alternate_name:
              - Batman and Batgirl
              - Batman and Catwoman
              - Batman and Nightwing
              - Batman and Red Hood
              - Batman and Red Robin
        - Edge of Spider-Verse
        - Herobear And The Kid Saving Time
        - Infinite Crisis(.*)Fight for the Multiverse
        - Futurama Comics
        - Manifest Destiny
        - Wolf Moon

        # Image
        - Sidekicks:
            begin: 8

        # Marvel
        - The Death of Wolverine # Mini-series 1-4
        - Spider-Man 2099:
            begin: 3

        # Titan Publishing
        - Doctor Who The Eleventh Doctor # Miniseries        

  Bunch-O-Comics:
    inputs:
      - rss: http://kickass.to/usearch/category%3Acomics%20user%3ANemesis43%20seeds%3A100/?rss=1
    set:
      path:  D:/Blackhole/Torrents/Comics/    
    if:      
      - "'magnet' not in url.lower()":
          download: yes
      - "'magnet' in url.lower()":
          exec: 'echo "{{url}}" > "D:/Blackhole/Torrents/Comics/{{title}}.magnet"'
    torrent_alive: yes    
    manipulate:
      - title:
          replace:
            regexp: 'annual (\d){1,4}'
            format: 'Special A\1'
      - title:
          replace:
            regexp: 'special (\d){1,3}'
            format: 'Special SP\1'

  WWE-Raw:
    inputs:
      - rss: http://xtremewrestlingtorrents.net/rss.php?feed=dl&cat=51:COOKIE:uid=757956;pass=f12a628f6b0673b4b62e40e343c37e69
      - rss: http://xtremewrestlingtorrents.net/rss.php?feed=dl&cat=53:COOKIE:uid=757956;pass=f12a628f6b0673b4b62e40e343c37e69
      - rss: http://xtremewrestlingtorrents.net/rss.php?feed=dl&cat=63:COOKIE:uid=757956;pass=f12a628f6b0673b4b62e40e343c37e69
      - rss: http://xtremewrestlingtorrents.net/rss.php?feed=dl&cat=50:COOKIE:uid=757956;pass=f12a628f6b0673b4b62e40e343c37e69
    template: wrestling-common
    regexp:
      reject:
        - german
    series:
      - Monday Night Raw:
          quality: 720p
          name_regexp:
            - Monday\.Night\.Raw
            - WWE\.Monday\.Night\.Raw
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
            - uiwATa3P8esXjPRqf66A45uYmWJWfF
        apikey: aqg1jyzhxj5dQbP43xdUwpBAXiBhq5
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
        - \WIta\W
        - \WFr\W
        - \WSpa\W
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
        - Key & Peele:
            alternate_name:
              - Key and Peele
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

```