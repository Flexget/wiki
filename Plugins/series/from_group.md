== Specify group (eg. anime fansubs) ==

'''Example:'''

{{{
series:
  - fullmetal alchemist brotherhood:
      from_group: eclipse
  - naruto:
      from_group:
        - horriblesubs
        - crunchysubs
}}}

'''Supported notations:'''

 * [Group] Series
 * Series XviD-Group

To disallow certain groups use [wiki:Plugins/regexp regexp] plugin to reject them.
