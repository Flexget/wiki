# Special IDs

Define other terms on top of the default 'special' which will cause a release in this series to be flagged as a special.

Example:
```
series:
  - My Series:
      special_ids: short
```

If more than one is desired, the option can be specified as a list:
```
series:
  - The Show:
      special_ids:
        - short
        - OVA
```
