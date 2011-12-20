= Use pogdesign.co.uk as input for import_series =

This feed will pull your series from [http://www.pogdesign.co.uk/cat pogdesign.co.uk/cat] using [wiki:Plugins/import_series import_series]

First you need to set up your account at pogdesign.co.uk and select your series. Then you need to locate the iCal-url (Hint: "Download iCal file"). It will look like this: http://pogdesign.co.uk/cat/download_ics/<a bunch of letters and numbers>

{{{
presets:
  tv:
    import_series:
      settings:
        min_quality: dsr
        max_quality: 720p
        quality: 720p
        timeframe: 2 hours
      from:
        text:
          url: <your url>
          entry:
            title: ^SUMMARY:(.*) [0-9]+x[0-9]+.*$
            url: ^SUMMARY:(.*) [0-9]+x[0-9]+.*$
feeds:
  tv:     
    inputs:
      - rss: http://feed1.com
      - rss: http://feed2.com
    preset:
      - tv
}}}