= Parsing =

Flexget often have to analyze raw text from your input sources. It gives proper information from file/release name, like name, title, year, quality, ... This processing is called parsing.

`parsing` plugin allow to configure the parser used for movie and series parsing. 

There are actually two parsers:
- `internal`: Historical and default parser used by flexget.
- `guessit`: Integration of a [https://www.github.com/wackou/guessit standalone project] dedicated to parsing. It's able to guess most information from any movie or series filename/release name. 

If you have IMDB/TMBD lookup failures and some movie or series that "slip through the net", you should really consider using `guessit` instead of `internal` parser.

=== Example ===

To enable `guessit` for movie and series parsing:

{{{
parsing:
  movie: guessit
  series: guessit
}}}