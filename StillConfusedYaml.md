---
title: StillConfusedYaml
description: 
published: true
date: 2022-09-18T04:51:45.715Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:43.072Z
---

## Still confused about Yaml?
Please note that each indentation level must be precisely **2 spaces**. Tabs are forbidden for indentation. Why are indentation even required in Yaml? It is used for semantics or **relation**. Consider example:

```
pets:
  cat:
    name: furry
    age: 5
  dog:
    name: barky
    age: 2
    toys:
      - bone
      - ball
```

Here we have two pets, cat and dog. Each of them has name, and age. Dog has list of toys. If we were to use more conventional configuration file format it would be much messier to represent complex relations.

Some other configuration files might represent previous example in following form:

```
pets.cat.name=furry
pets.cat.age=5
pets.dog.name=barky
pets.dog.age=2
pets.dog.toys=bone, ball
```

But consider more complex situation ...

```
pets:
  dog:
    name: barky
    age: 2
    toys:
      - ball:
          color: blue
          size: 70mm
      - bone:
          dimensions:
            length: 10cm
            height: 2cm
          taste: chicken
```

And you have nice mess in your hands ...