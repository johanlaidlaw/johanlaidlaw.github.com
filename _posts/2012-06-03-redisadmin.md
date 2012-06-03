---
layout: post
title: "RedisAdmin"
description: "User interface for Redis"
category:
tags: [RedisAdmin, Redis]
---
{% include JB/setup %}

We have used Redis at work for quite some time and when we started to use it I could see right away that it would be useful with a friendly user interface. It can be a bit cumbersome to use the cli when you have to debug fields. You always need to know the type of the field and the command of getting/setting the value.

So I build RedisAdmin.

It's a simple user interface where you can search for keys and edit/delete values.
Key features which we have found very useful:

 - Quick search for keys
 - Easy expand a key no matter what type it is
 - Members are ordered alphabeticly when expanding a Hash
 - Easy edit a value no matter of type


You just need to clone/fork it from [https://github.com/johanlaidlaw/Redisadmin](https://github.com/johanlaidlaw/Redisadmin) and place it in a web directory.



