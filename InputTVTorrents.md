= TVTorrents =

A customized HTML input module. Parses out full torrent URLs from [http://tvtorrents.com TVTorrents]' page for recently aired TV show episodes.

May break in the future, as it depends on the exact structure of the HTML.

Module-specific code by Fredrik Bränström.

== Usage ==

Just set '''tvt: true''' in your config, and provide the path to your login cookie by using the cookies module.

== Example ==

{{{
feeds:
  TVTorrents:
    tvt: true

    cookies:
      type: mozilla
      file: ~/.mozilla/firefox/profile/cookies.txt
}}}

Note: Of yourse, you need to configure a '''patterns''' filter to match only desired content. The '''series filter does NOT''' appear to work well with this module yet - just use a pattern like (lost|csi).*?720p until we figure out why.

== Example with pattern ==

{{{
feeds:
  TVTorrents:
    tvt: true

    cookies:
      type: mozilla
      file: ~/.mozilla/firefox/profile/cookies.txt

    patterns:
      - ^(house|battlestar galactica|csi ).*?720p
    ignore:
      - INDI

    download: ~/Downloads
}}}

This would download all new torrent files for shows House, Battlestar Galactica and CSI, in 720p quality.
