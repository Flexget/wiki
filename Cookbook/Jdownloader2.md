---
title: Jdownloader2
description: 
published: true
date: 2022-09-18T04:55:40.180Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:37.615Z
---

You can use JDownloader2 as output.

Activate Jdownloader2's folderwatch function and use the exec plugin in flexget.


example:
```
tasks:
  task_name:
    rss: http://example.com
    series:
      - Lost
      - Another Show
    exec: 
      - echo text={{url}} >> "/path/to/folderwatch/{{title}}.crawljob"
      - echo downloadFolder=/path/to/Downloads/{{title}} >> "/path/to/folderwatch/{{title}}.crawljob"
      ##if you also need to parse the content of the url, uncomment following line
      #- echo deepAnalyseEnabled=true >> "/path/to/folderwatch/{{title}}.crawljob"
```

folderwatch is located by default inside the JDownloader2 installation folder

these are the changeable values:
```
#a comment
   extractPasswords=["Password1","Password2"](/"Password1","Password2")
   enabled=null
   text=http://www.hornoxe.com/kreuzfahrtschiff-wird-verlaengert-zeitraffer/
   packageName=MyPackageName
   autoStart=TRUE
   extractAfterDownload=UNSET
   downloadFolder=null
   priority=DEFAULT
   forcedStart=UNSET
   downloadPassword=null
#use only if text contains one single link
   filename=null
   overwritePackagizerEnabled=false
   comment=null
   autoConfirm=UNSET
   deepAnalyseEnabled=false
   addOfflineLink=true

->NEW ENTRY<-
#properties that are not required can be ignored. This is absolutly fine:
   text=http://www.hornoxe.com/katze-nimmt-die-post-entgegen/


### Available Fields:

# enabled Type: BooleanStatus
# enabled = null
# comment Type: String
# comment = null
# priority Type: Priority
# priority = null
# text Type: String
# text = null
# chunks Type: int
# chunks = 0
# downloadPassword Type: String
# downloadPassword = null
# type Type: JobType
# type = NORMAL
# downloadFolder Type: String
# downloadFolder = null
# overwritePackagizerEnabled Type: boolean
# overwritePackagizerEnabled = true
# packageName Type: String
# packageName = null
# filename Type: String
# filename = null
# autoStart Type: BooleanStatus
# autoStart = UNSET
# addOfflineLink Type: boolean
# addOfflineLink = true
# autoConfirm Type: BooleanStatus
# autoConfirm = UNSET
# forcedStart Type: BooleanStatus
# forcedStart = UNSET
# extractAfterDownload Type: BooleanStatus
# extractAfterDownload = UNSET
# extractPasswords Type: String[]
# extractPasswords = null
# deepAnalyseEnabled Type: boolean
# deepAnalyseEnabled = false
```
