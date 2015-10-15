= Filesystem =
Uses local path content as an input. Generate entries from files, dirs & symlinks found in path(s). [[BR]]
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''path'''||One or more paths. Must be unique. Mandatory when using an object in config.||
||'''mask'''||File mask, like '*.mkv'  ||
||'''regexp'''||Regexp like `.*\.(avi|mkv)$`. Note: If both `mask` and `regexp` are present, `mask` will be used. ||
||'''recursive'''||Recursion flag. Can be set to `True`, `False` or an integer. `True` will recurse without limit, `False` will not recurse and the integer value will decide how deep the recursion should go (minimum is 1 level deep, which is similar to no recursion. Default is `False`||
||'''retrieve'''||Decided which type of objects should be made into entries. Accepts one or more of the following: `files`, `dirs` `symlinks`. Default is all of them.  ||
}}}

It isn't necessary to send an object including parameters, there are many acceptable permutations. See examples below:
    
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