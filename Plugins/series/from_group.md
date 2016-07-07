## Specify group (eg. anime fansubs)
**Example:**

```
series:
  - fullmetal alchemist brotherhood:
      from_group: eclipse
  - naruto:
      from_group:
        - horriblesubs
        - crunchysubs
```

**Supported notations:**

 * [Group](/Group) Series
 * Series XviD-Group

To disallow certain groups use [regexp](/Plugins/regexp) plugin to reject them.
