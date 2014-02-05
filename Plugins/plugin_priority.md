= Plugin priority =

Each plugin has default priority which usually makes the most sense, however in some cases you may want to run particular plugin before another. With priority plugin you can change default priority values in a task. Higher values are execute first. You can use `flexget plugins` to view default priorities.
[[BR]][[BR]]
        
'''Example:'''

{{{        
plugin_priority:
  series: 240
  manipulate: 250
}}}