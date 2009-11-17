= Download Heroes comics =

Download all/new heroes comics from [http://nbc.com/Heroes nbc.com]. This uses advanced text-parsing plugin and does not represent accurately average usage.

{{{
feeds:
  heroes:
    interval: 6 hours
    text:
      url: http://www.nbc.com/Heroes/js/novels.js
      entry:
        title: novelTitle = "(.*)"
        url: novelPrint = "(.*)"
      format:
        url: http://www.nbc.com%(url)s
    download: ~/heroes/
}}}

Uses plugins: [wiki:ModuleInterval interval], [wiki:InputText text], [wiki:OutputDownload download]

[wiki:Cookbook Back to The Cookbook]