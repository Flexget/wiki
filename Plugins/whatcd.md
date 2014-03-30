= Whatcd =

A plugin that performs searches on [https://what.cd] and returns entries for each result.

== Usage ==

All parameters except `username` and `password` are optional.

{{{
whatcd:
    username:
    password:

    user_agent: (A custom user-agent for the client to report.
                 It is NOT A GOOD IDEA to spoof a browser with
                 this. You are responsible for your account.)

    search: (general search filter)

    artist: (artist name)
    album: (album name)
    year: (album year)

    encoding: (encoding specifics - 192, 320, lossless, etc.)
    format: (MP3, FLAC, AAC, etc.)
    media: (CD, DVD, vinyl, Blu-ray, etc.)
    release_type: (album, soundtrack, EP, etc.)

    log: (log specification - true, false, '100%', or '<100%')
    hascue: (has a cue file - true or false)
    scene: (is a scene release - true or false)
    vanityhouse: (is a vanity house release - true or false)
    leech_type: ('freeleech', 'neutral', 'either', or 'normal')

    tags: (a list of tags to match - drum.and.bass, new.age, blues, etc.)
    tag_type: (match 'any' or 'all' of the items in `tags`)
}}}