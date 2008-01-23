= Download =

Downloads content from entry url and writes it into a file.
Simple example:

download: ~/torrents/

Advanced users:

Some modules may set alternative download path for entry.
Prime example is module patterns that can be used to override path.

Configuration example:

{{{
pattenrs:
  - pattern1
  - pattern2
  - pattern3: ~/another_location/
download: ~/torrents/
}}}

This results that entries matching patterns 1 and 2 are saved into
~/torrents/ and pattern3 is saved to ~/another_location/.