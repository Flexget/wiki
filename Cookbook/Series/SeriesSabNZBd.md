= Series name as a category =

When using [wiki:Plugin/sabnzbd sabnzbd] you can use series name as a category by utilizing [wiki:Plugin/set set] plugin. The category name will be exactly the one written in as a series name.

{{{
feeds:
  my-feed:
    .
    .
    series:
      720p: 
        quality: 720p
        set:
          category: %(series_name)s

      720p
        - chuck
        - south park

    sabnzbd:
      key: 1234567890
}}}

[wiki:TheCookBook Back to The Cookbook]