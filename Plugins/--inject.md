= Inject =

Allows injecting imaginary entry for FlexGet to process.

'''Syntax:'''

{{{        
--inject <title>
}}}
        
Random url will be generated. All other inputs are disabled.

'''Example use:'''
        
{{{
flexget --inject "Some.Series.S02E12.Imaginary" --feed my-series --learn
}}}
        
This would inject imaginary series into a single feed and learn it as a downloaded,
assuming feed accepts the injected entry.