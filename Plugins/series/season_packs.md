# Season packs

## This IS NOT released yet, just a placeholder!

This option can be used if you want to accept season packs in addition to (or instead) of episodes. At this time, only `ep` [identified](Plugins/series/identified_by) shows can accept season packs.

## Usage:

There are several modes of usage for this option. 

#### Basic usage:
```yaml
season_packs: yes
```
This will enable accepting season packs for any series that did not download ANY episodes for that particular season.  

#### Example:
```yaml
tasks:
  series_task:
    rss: bla
    series:
    - Foo:
        season_packs: yes
    download: '/shows/{{ series_name }}'
```

Let's say you have a show name `Foo` which you have downloaded an episode already for season `1`. Now your task encounters the following file:
`Foo.S01.720p.HDTB-Flexget`. 

Setting `season_packs: yes` means "accept season packs for this show as long as no more than **0** episodes have been downloaded for this season". The idea is not to accept a season pack for a season which you have already have started to track induvidual episodes for.  
An alternate way to acheive the **exact** same behaviour as this is to set the config like this:
```yaml
tasks:
  series_task:
    rss: bla
    series:
    - Foo:
        season_packs: 0
    download: '/shows/{{ series_name }}'
```
The number `0` after season packs refers to the number of episodes each season is allowed to previously download before accepting a season pack. 

#### Manually specifying threshold:
In case you want to manipulate the number of allowed episodes when accepting a season pack, you can specify it like so:
```yaml
season_packs: 10
```
This will allow downloading up to to 10 episodes per season (in any order) and also accepting a season pack of the same season.

#### Ignoring episode threshold:
In case you do not care about setting an episode threshold, and would like to always accept a season pack regardless of how many episdoes were already downloaded for that particular series, use the following option:
```yaml
season_pack: always
```

#### Accepting only season packs:
In case you want to accept **only** season pack for a series, use the following option:
```yaml
season_packs: only
```
### Important Note: 
In all cases and modes, once a season pack is accepted, that particular season will be marked as completed, **and no more seasons or episodes for that particular season would be accepted.**

