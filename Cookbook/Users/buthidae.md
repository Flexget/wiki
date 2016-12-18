**Current version - 1.2.258**

This config runs tasks to perform the following actions:

1) Grab an RSS feed, download desired series from it, and download the .torrent files to a watched folder
2) Grab an RSS feed, download all items from it, and download the .torrent files to a watched folder
3) Use the [AutomaticRarUnpack](https://flexget.com/wiki/Cookbook/AutomaticRarUnpack) recipe to check the seeding folder for .rar files, and extract them to a "new videos" folder
4) Check the seeding folder for completed .avi, .mkv. or .mp4 files, and copy them to a "new videos" folder
5) Check the "new videos" folder for TV show files, and clean up the naming style

The config is styled towards running on Mac OS X, but should be easily modified for any OS.

Each task will send a Prowl notification on completion. A secrets file is used for confidentiality and ease of repetition.

Some TV show files on my site-of-choice come named *series.name.xyy.quality.ext* instead of *series.name.SxxEyy.quality.ext*. The "Rename Copied TV Shows" task uses regexp supplied by the "renameshows" template to reformat everything to *Series Name.SxxEyy.quality.ext*. Because it places the renamed file in to the same folder, the [Seen plugin](https://flexget.com/wiki/Plugins/seen) actions the file twice. You could move the files to another folder to avoid this - I've chosen not to. Seen is also run in local mode to avoid messing up episode order or erroneously skipping files.

Finally, because we have a [Mac OS X LaunchAgent](https://flexget.com/wiki/InstallWizard/OSX) calling the script every 15 minutes, the [Secheduler](https://flexget.com/wiki/Plugins/Daemon/scheduler) plugin is turned off.

I've put in lots of comments on stuff that I struggled with while I was learning :-)

```
secrets: secretfile.yml
# Running on OS X via launchd, so the scheduler is disabled
schedules: no
# Set schedules to yes and uncomment below for constantly-running process
#  - tasks: '*'
#    interval:
#      minutes: 15
templates:
  tv:
    download: ~/Downloads/AutoDownload/
    exists_series: 
      - /Volumes/Three over Two/TV Shows/
      - ~/Desktop/Downloaded Videos/
# The main shows to download go here
  shows:
    series:
      list:
        - Castle
        - Chicago Fire
        - Chicago PD
        - Cougar Town
        - Criminal Minds
        - Episodes
        - Franklin and Bash
        - Last Week Tonight
        - Modern Family
        - Once Upon a Time
        - Shaun Micallefs Mad as Hell
        - Silicon Valley
        - Suits
        - The Big Bang Theory
        - The Chasers Media Circus
        - The Newsroom
        - The Originals
        - The Vampire Diaries
        - True Blood
        - Two and a half Men
        - Upper Middle Bogan
# We need a separate list here with the regexp for numeric episode IDs
# This is to stop it interfering with automatic downloads which usually have SxxEyy
  renameshows:
    series:
      settings:
        list:
          ep_regexp:
# Some shows (e.g. Castle) have a YYYY designation (i.e. Castle (2009). We handle this like so:
            - \d\d\d\d.(\d\d)(\d\d)
            - \d\d\d\d.(\d)(\d\d)
# Match four-digit - SSee - 0312, 1315
            - (\d\d)(\d\d)
# Then match three-digit - See - 213
            - (\d)(\d\d)
# Don't care about the last seen episode
          parse_only: yes
# We can also add shows here that we only download ad-hoc
      list:
        - The Simpsons

# Previous config for email alerts
#  global:
#    email:
#      from: FROM_ADDRESS
#      to: TO_ADDRESS
#      smtp_host: MAIL_HOST
#      smtp_port: 25
#      smtp_login: true
#      smtp_username: '{{ secrets.mail.usr }}'
#      smtp_password: '{{ secrets.mail.pwd }}'

tasks:
  Site x264 SD Downloads:
    rss: https://site/torrents/rss?u={{ secrets.site.usr }};tp={{ secrets.site.pwd }};l79;download
    template: 
      - tv
      - shows
    prowl:
      apikey: {{ secrets.prowl.key }}
      event: New Show Downloaded
  Site Bookmarked:
    rss: https://site/torrents/rss?u={{ secrets.site.usr }};tp={{ secrets.site.pwd }};bookmarks;download
    accept_all: yes
    template: tv
    prowl:
      apikey: {{ secrets.prowl.key }}
      event: Bookmarked File Downloaded
# Only need to run this initially
  seed_series_db:
    find:
      regexp: .*(avi|mkv|mp4)$
      path: 
        - /Volumes/Three over Two/TV Shows/
        - ~/Desktop/Downloaded Videos/
      recursive: yes
    template: shows
    manual: yes
  Extract RAR:
    inputs:
      - find:
          path:
            - ~/Desktop/Completed
          mask: '*.rar'
          recursive: yes
# This regexp will grab anything .rar, implicitly ignoring .r01/.r02/etc. We need to tell it to avoid part02/03/etc.rar. If the "Never overwrite" (-o-) flag
# isn't set, the script will hang waiting for input, and will have to be manually terminated. You could set "Overwrite" (-o+) or "Yes to prompt" (-y) instead.
    regexp:
      accept_excluding:
        - part([0-9](/0-9){2,4}|[2-9](/2-9)).rar$
      accept:
        - part01.rar$
        - part001.rar$
      from: location
    only_new: yes
    exec:
      allow_background: no
      auto_escape: no
      fail_entries: yes
      on_output:
        for_accepted: >
          unrar e -o- "{{location}}" "/Users/localadmin/Desktop/Downloaded Videos"
    prowl:
      apikey: {{ secrets.prowl.key }}
      event: Extracted RAR File
  Completed Video Files:
    inputs:
      - find:
          path:
            - ~/Desktop/Completed/
          recursive: yes
          regexp: .*(mp4|mkv|avi)$
    regexp:
      reject:
        - sample
    accept_all: yes
    exec:
      allow_background: no
      auto_escape: no
      fail_entries: yes
      on_output:
        for_accepted: >
          cp "{{location}}" "/Users/localadmin/Desktop/Downloaded Videos"
    prowl:
      apikey: {{ secrets.prowl.key }}
      event: Copied Completed File

  Rename Copied TV Shows:
    template:
      - shows
      - renameshows
    inputs:
      - find:
          path:
            - ~/Desktop/Downloaded Videos/
          regexp: .*(mp4|mkv|avi)$
          recursive: no
    accept_all: yes
    thetvdb_lookup: yes
    seen: local
# Ignore non-TV Show files
    require_field: [series_id](/series_id)
    all_series:
      parse_only: yes
    move:
      filename: "{{ series_name }}.{{ series_id }}.{{ tvdb_ep_name|default('Unknown') }}.{{ quality|upper }}"
    prowl:
      apikey: {{ secrets.prowl.key }}
      event: Renamed File
      description: Renamed "{{ series_name }}.{{ series_id }}"
```