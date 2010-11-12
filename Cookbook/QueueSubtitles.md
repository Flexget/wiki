For subtitle sites that have a rss feed on newly added subtitles you can abuse a multi database setup to handle the subtitles download.

Basicly, the series filter should keep two different databases, one for the video and another for the subtitle, so it doesn't rejects wathever entry comes last; AND the movies feed uses exec to queue imdb entries that are later downloaded from the subtitles feed.

This assumes that movies releases are seen by flexget before the subtitles releases, which is usually the case.

tv.yml:
{{{
series:
  hdtv:
    - Weeds
    - Heroes
    - Lost
    - The IT Crowd
}}}

series.yml
{{{
presets:
  tv:
    include: tv.yml

feeds:
  rss_tv:
    rss: http:// ...
    preset: tv
    download: ~/Download
}}}

movies.yml
{{{
feeds:
  movies:
    rss: http:// ...
    imdb_queue: yes
    imdb:
      ...
    download: ~/Download
    exec: flexget -c legendas.yml --imdb-queue add %(imdb_url)s
}}}

legendas.yml
{{{
presets:
  tv:
    include: tv.yml
  legendas:
    form:
      url: http:// ...
      userfield: ...
      passfield: ...
      username: xxx
      password: xxx
    urlrewrite:
      legendas:
        regexp: ...
        format: ...

feeds:
  series_subs:
    rss: http:// ...
    preset:
      - tv
      - legendas
    download: ~/Download
  movies_subs:
    rss: http:// ...
    preset: legendas
    imdb_queue: yes
    download: ~/Download

}}}