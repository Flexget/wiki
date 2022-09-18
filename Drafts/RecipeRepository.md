---
title: RecipeRepository
description: 
published: true
date: 2022-09-18T04:58:21.238Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:18.600Z
---


## Rationale
It's impossible to have sane defaults that suit everyone. At the same time, having extensive configurability makes for a steep learning curve that not everyone wants to go through.

But there's a way to provide both user-friendliness and complete cutomizability: a template repository.

## What's a recipe
A recipe is a set of sane defaults with few configuration options. Through a GUI, the user should be able to choose a **single** *base* recipe for each task. A recipe might call another sub-recipe of certain category, e.g. output, filtering, etc. So, after adding a new task, something like this might appear:


|   <img src="http://i6.minus.com/i1jHjOYdm7ga6.png">   |
| --- |
|   *Mockup of the UI. Advanced Configuration points to the fancy [[Drafts/ConfigEditor]].*   |



After choosing a base recipe the task's configuration might look like this:

|   <img src="http://i4.minus.com/ibpUcn5jx9BAW6.png">   |
| --- |


Notice at the bottom how output is defined by another recipe. Once chosen, the *sub-recipe* should display its options indented in the same page that the *base* recipe does.
