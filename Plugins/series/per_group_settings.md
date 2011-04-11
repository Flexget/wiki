== Group settings ==

Many times, you will want to apply a setting to more than one show at once. In this instance, you can use a more advanced config format, to define groups, and settings that apply to the whole group.

{{{
series:
  [settings]:
    [group name]:
      [setting]: [value]
  [group name]:
    - first series
    - second series
}}}

An example, setting [wiki:Plugins/series/propers propers] for ''group 1'':

{{{
series:
  settings:
    group 1:
      propers: 3 days
  group 1:
    - Series 1
    - Series 2
  720p:
    - Series 3
    - Series 4:
        quality: 1080p
  normal:
    - Series 5
}}}

Notes:

 * The names of the groups are arbitrary, so you can pick whatever you want.[[BR]]
 In this example ''normal'' is just a group without any options.
 * If a group name is a quality, it will automatically have that as a quality.[[BR]]
 In this example ''Series 3'' has it's quality set to 720p, because 720p is a [wiki:Plugins/quality#Supportedqualities known quality name.]
 * Series may override any settings specified in group settings.[[BR]]
 In this example ''Series 4'' overrides the quality setting of it's group with 1080p.