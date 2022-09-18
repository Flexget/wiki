---
title: Johny-O-Rourke
description: 
published: true
date: 2022-09-18T04:50:21.633Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:50:18.873Z
---

templates:
  mma:
    sabnzbd:
  key: 123456
  url: http://localhost/sabnzbd/api?
  category: movieswrite:
      demonoid:
        regexp: https://www.demonoid.pw/files/details/(?P<id>\d+)/
        format: https://www.demonoid.pw/files/download/\g<id>/
    headers:
      user-agent: QQQ"Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"QQQ
    cookies:
      file: QQQ/home/username/.flexget/cookies.sqliteQQQ
    rss: https://www.demonoid.pw/rss/users/mich00.xml

tasks:
  UFC main event task:
    template: mma
    regexp:
      from: title
      reject:
        - (early|weigh|embedded|night|fox|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|prelim|history|post.fight|press.conference|preview|greatest.fighters|fame)
    series:
      - UFC:
          identified_by: sequence
          quality: 720p
          
  UFC prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d\d.prelim)
      from: title
      reject:
        - (early|weigh|embedded|night|fox|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'ufc'
            format: 'ufc prelim'
    series:
      - UFC prelim:
          identified_by: sequence
          quality: 720p

  UFC early prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d\d.early)
      from: title
      reject:
        - (weigh|embedded|night|fox|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'ufc'
            format: 'ufc early prelim'
    series:
      - UFC early prelim:
          identified_by: sequence
          quality: 720p

  MMA main event task:
    template: mma
    regexp:
      from: title
      reject:
        - (weigh|early|prelim|embedded|super.fight|superfight|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    series:
      - UFC on Fox:
          identified_by: sequence
          quality: 720p
      - UFC Fight Night:
          identified_by: sequence
          quality: 720p
      - Bellator:
          identified_by: sequence
          quality: 720p
      - LFA:
          alternate_name: Legacy Fighting Alliance
          identified_by: sequence
          quality: 720p
      - Invicta FC:
          identified_by: sequence
          quality: 720p
      - Glory:
          identified_by: sequence
          quality: 720p
      - One Championship:
          identified_by: sequence
          quality: 720p
      - Titan FC:
          identified_by: sequence
          quality: 720p
      - WSOF:
          alternate_name: World Series of Fighting
          identified_by: sequence
          quality: 720p

  UFC on Fox prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d.prelim)
      from: title
      reject:
        - (early|weigh|embedded|night|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'ufc on fox'
            format: 'ufc on fox prelim'
    series:
      - UFC on Fox prelim:
          identified_by: sequence
          quality: 720p

  UFC on Fox early prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d.early)
      from: title
      reject:
        - (weigh|embedded|night|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'ufc on fox'
            format: 'ufc on fox early prelim'
    series:
      - UFC on Fox early prelim:
          identified_by: sequence
          quality: 720p

  UFC Fight Night prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d\d.prelim)
      from: title
      reject:
        - (early|weigh|embedded|fox|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'ufc fight night'
            format: 'ufc fight night prelim'
    series:
      - UFC Fight Night prelim:
          identified_by: sequence
          quality: 720p

  UFC Fight Night early prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d\d.early)
      from: title
      reject:
        - (weigh|embedded|fox|ultimate|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'ufc fight night'
            format: 'ufc fight night early prelim'
    series:
      - UFC Fight Night early prelim:
          identified_by: sequence
          quality: 720p

  The Ultimate Fighter Finale main event task:
    template: mma
    regexp:
      reject_excluding:
        - finale
      from: title
      reject:
        - (early|prelim|weigh|embedded|fox|night|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    series:
      - The Ultimate Fighter:
          identified_by: sequence
          quality: 720p

  The Ultimate Fighter Finale prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (/d/d.finale.prelim)
      from: title
      reject:
        - (early|weigh|embedded|fox|night|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'the ultimate fighter'
            format: 'the ultimate fighter prelim'
    series:
      - The Ultimate Fighter prelim:
          identified_by: sequence
          quality: 720p

  The Ultimate Fighter Finale early prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (/d/d.finale.early)
      from: title
      reject:
        - (weigh|embedded|fox|night|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'the ultimate fighter'
            format: 'the ultimate fighter early prelim'
    series:
      - The Ultimate Fighter early prelim:
          identified_by: sequence
          quality: 720p

  Bellator prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d\d.prelim)
      from: title
      reject:
        - (early|weigh|embedded|fox|night|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'Bellator'
            format: 'Bellator prelim'
    series:
      - Bellator prelim:
          identified_by: sequence
          quality: 720p

  WSOF prelim event task:
    template: mma
    regexp:
      reject_excluding:
        - (\d\d.prelim)
      from: title
      reject:
        - (early|weigh|embedded|fox|night|dana|breakdown|the.fly|inside|road|vlog|now|countdown|history|post.fight|press.conference|preview|greatest.fighters|fame)
    manipulate:
      - title:
          replace:
            regexp: 'WSOF'
            format: 'WSOF prelim'
          replace:
            regexp: 'World Series of Fighting'
            format: 'WSOF prelim'
    series:
      - WSOF prelim:
          alternate_name: World Series of Fighting prelim
          identified_by: sequence
          quality: 720p

  UFC Now task:
    template: mma
    regexp:
      reject_excluding:
        - (ep.\d)
    manipulate:
      - title:
          replace:
            regexp: 'UFC.Now.Ep.4'
            format: 'UFC Now S04E'
    series:
      - UFC Now:
          quality: 720p