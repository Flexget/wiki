---
title: duplicates_and_nukes
description: 
published: true
date: 2022-09-18T05:21:48.923Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:45.614Z
---

This recepie scans filesystem for duplicates, nuked releases and lesser quality outputting a list of directories that can be deleted to a file.

    tasks:
      dups:
        assume_quality:
          h264: 480p
        configure_series:
          from:
            filesystem: /mnt/tv
        filesystem:
          path:
            - /mnt/tv
          recursive: yes
          retrieve: dirs
        if:
          - has_field('series_episode'):
              exec:
                on_output:
                  for_undecided: echo {{series_name}} {{series_id}} {{quality}}  {{location}} >> `date +%y%m%d`.dups.out