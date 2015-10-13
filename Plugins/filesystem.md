= Filesystem =
Uses local path content as an input.[[BR]]
Can use recursion if configured. Recursion is False by default.[[BR]]
Can be configured to true or get integer that will specify max depth in relation to the base folder.[[BR]]
All files/dir/symlinks are retrieved by default. Can be changed by using the 'retrieve' property.

    
== Examples ==

=== Single path ===      
{{{
      filesystem: /storage/movies/
}}}


    
=== List of paths ===
{{{
      filesystem:
         - /storage/movies/
         - /storage/tv/
}}}

=== Object with list of paths ===
{{{
      filesystem:
        path:
          - /storage/movies/
          - /storage/tv/
        mask: '*.mkv'
}}}

=== Using Recursion ===
{{{
      filesystem:
        path:
          - /storage/movies/
          - /storage/tv/
        recursive: 4  # 4 levels deep from each base folder
        retrieve: files  # Only files will be retrieved
}}}

=== Extended Recursion ===
{{{
      filesystem:
        path:
          - /storage/movies/
          - /storage/tv/
        recursive: yes  # No limit to depth, all sub dirs will be accessed
        retrieve:  # Only files and dirs will be retrieved
          - files
          - dirs
        regexp: '.*\.(avi|mkv|mp4|m4v|iso)$'
}}}