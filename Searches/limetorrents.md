# Limetorrents
This search plugin will get results from [http://limetorrents.in](http://limetorrents.in)

## Configuration
Simply enable the plugin:
```
limetorrents: yes
```

You can specify a single category:
```
limetorrents:
  category: movies
```

## List of possible categories
* `all`
* `anime`
* `applications`
* `games`
* `movies`
* `music`
* `tv`
* `other`

You can also specify the sorting of the entries:
```
limetorrents:
  order_by: date
```
This can be either `date` or `seeds`.

Category defaults to `all` and order_by to `date` if none is specified.