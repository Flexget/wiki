# Html
Parses URLs from html page. Useful on sites which have direct download links of any type (mp3, jpg, torrent, ...).

Many anime-fansubbers do not provide an RSS-feed, this usually works for those cases.

### Example
```
html: <url>
```

Note: This returns ALL links from the page so you need to configure some filters to match only to desired content.

### Example with regexp
```
html: <url>
regexp:
  accept:
    - podcast.*\.mp3
  rest: reject
```

This would download all links that have mp3 link with word podcast in them.

## Title options
By default html plugin will try to guess where link titles should be captured from but in some cases this goes wrong and you end up with useless titles like 'DL', '1', '2'. In case automatic selection does not work you will need to specify where titles should be captured from. Note that it may not always be possible to get good titles if the the title is nowhere near the link.

### Example
```
html:
  url: <url>
  title_from: url
```

Other possible values are: `auto` *(default)*, `url`, `title` and `link`. 

### Example: url
If captured URL is `http://some.domain.com/download/Podcast.2010-01-02.mp3` the extracted title would be "Podcast.2010-01-02.mp3"

### Example: title
If html contains links in form of `<a href="http://some.domain.com/download?id=1245932" title="Podcast.2010-01-02.mp3">Download</a>` the extracted title would be "Podcast.2010-01-02.mp3"

### Example: link
If html contains links in form of `<a href="http://some.domain.com/download?id=1245932">Podcast.2010-01-02.mp3</a>` the extracted title would be "Podcast.2010-01-02.mp3"

## Titles are gibberish
In some cases the titles are completely useless, however you may still get good filenames when entry is downloaded. This is because servers often send the correct filename in http headers. Of course when titles are useless filtering becomes much more troublesome.

## Get only certain links
In case page contains too many links, you can use regexps to select only certain links.

### Example
```
html:
  url: <url>
  links_re:
    - domain\.com
```

This will create only entries from links which match any of given regexps. Do NOT use this for filtering content, just limit selecting to correct type of links and use real filtering plugins like [regexp](/Plugins/regexp) to do actual filtering.

## Basic Authentication
This plugin supports baisic authentication, it can be specified in the url:

```
html: http://username:password@url.com
```

Or as parameters:

```
html:
  url: <url>
  username: <username>
  password: <password>
```

## Dump
You can dump the received HTML into a file by using parameter `dump`. Useful for debugging.

### Example
```
html:
  url: <url>
  dump: file.html
```

## Increment
You can perform multiple request by using the increment option.

### Example
```
html:
  url: "www.somesite.com/search/?category=10&page={{i}}"
  increment: True
```

This will grab entries from 

```
www.somesite.com/search/?category=10&page=0
www.somesite.com/search/?category=10&page=1
www.somesite.com/search/?category=10&page=2
```

... and so on, until a total of 200 entries are retrieved, or no entry is retrieved on one request.

```
html:
  url: "www.somesite.com/search/?category=10&from={{i}}&to={{i+49}}"
  increment: 
    from: 0
    to: 10
    step : 50
```

This configuration will grab entries from those URLs

```
www.somesite.com/search/?category=10&from=0&to=49
www.somesite.com/search/?category=10&from=50&to=99
www.somesite.com/search/?category=10&from=100&to=149
www.somesite.com/search/?category=10&from=150&to=199
www.somesite.com/search/?category=10&from=200&to=249
www.somesite.com/search/?category=10&from=250&to=299
www.somesite.com/search/?category=10&from=300&to=349
www.somesite.com/search/?category=10&from=350&to=399
www.somesite.com/search/?category=10&from=400&to=449
www.somesite.com/search/?category=10&from=450&to=499
```

#### Additionnal increment Options

| **Option** | **Description** | **type** | **default** |
| --- | --- | --- | --- |
| from | Increment starting value | Number | 0 |
| to | If defined, plugin will stop when increment reach this value | Number | - |
| name | Name of the variable used in {{...}} jinja2 blocks | Text | "i" |
| step | The value that will be added to the variable, for each iteration (Can be negative) | Number | 1 |
| stop_when_empty | With `yes` plugin will stop when a page retrieves no entry | boolean | Yes |
||entries_count||If total entries count exceed this value, plugin will stop||Number||200||