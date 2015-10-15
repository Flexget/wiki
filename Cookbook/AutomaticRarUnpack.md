You can make some torrent clients (e.g. uTorrent) run this feed automatically each time the client has finished downloading something (In the case of utorrent its under Settings - Advanced - 'Run Program'). Or you can schedule it to check the download directories periodically.

{{{
# --Unrar feed---
# Unrars all files to another drive, windows platform 
# Mimics file structure, except for subtitle folders which are elevated to the previous folder

feeds:

  Extract:

    # Finds all rar files in the specified folder
    inputs:
      - filesystem:
          path: F:\Torrent\Completed
          mask: '*.rar'
          recursive: yes

    # Looks and accepts the first rar file of every archive set
    regexp:
      accept_excluding:
        - part([0-9]{2,4}|[2-9]).rar$
      accept:
        - part01.rar$
        - part001.rar$
    # Find plugin doesn't put the extension in the titles of entries, so we need to tell it to look at the location
      from: location

    # Disregard already processed files
    only_new: yes

    # Create output path for extraction, mimics filestructure from the folder "Completed"
    set:
      output_path: >
        {{ location|replace("F:\\Torrent\\Completed\\","E:\\Flexget\\Completed\\")|re_replace("\\\\Subs\\\\","\\\\")|re_replace("\\\\[^\\\\]*.rar","\\\\") }}

    # Send files to winrar to be unpacked, winrar must be installed to default path
    exec:
      allow_background: no
      auto_escape: no
      fail_entries: yes
      on_output:
        for_accepted: >
          "C:\Program Files\WinRAR\UnRAR.exe" x -o- -y "{{location}}" "{{output_path}}"
}}}

Paths are windows specific of course, but apart from that it should work for other platforms just fine.

For most *nix distributions, after coping unrar to your PATH and either modifying set.output_path or specifying an absolute path (as below) this should work:

{{{

      on_output:
        for_accepted: >
          unrar e -o- "{{location}}" "/Volumes/Media/Unsorted Videos"

}}}