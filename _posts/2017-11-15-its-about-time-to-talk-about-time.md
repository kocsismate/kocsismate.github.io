---
layout: post
title: "It's about time to talk about time"
date: 2017-11-15 20:00:00
categories: i18n
tags: timezone utc gmt
image: /assets/image/2017-11-15-/cover.jpg
---

Handling time correctly has always been one of the hardest problems in programming. Having been learned quite a few
interesting facts and practices about the topic, I'd like to summarize them in this blog post in the hope that others
also find them useful.

## The brief history of time systems

As an introduction, let's see the short history of the universal time system currently in use.
During the industrial revolution, Greenwich Mean Time (GMT) was created in Britain as an accurate time system became more
and more important. It can be surprising, but its name comes from the fact that the length of a GMT day is defined so that
the mean position of the Sun at noon for the whole year is directly above the Greenwich Meridian.

Later, it became clear that GMT is not accurate enough. It's because there are irregularities in the Earth's rate of
rotation. That's why in 1967, scientists developed another definition for the time, based on atomic terms:

> The second is the duration of 9,192,631,770 periods of the radiation corresponding to the transition between the two
hyperfine levels of the ground state of the caesium 133 atom.

It is called the SI second and it made possible for humanity to create the Coordinated Universal Time (UTC). UTC is
primarily used for scientific purposes, because only a handful of countries – including Australia, France, Germany and
The United States – apply it as their official time system.

You could wonder what the difference is between UTC and GMT then? Not much. In fact, UTC is not permitted to deviate from GMT
by more than 0.9 second. That's why leap seconds are occasionally added to the UTC time in order to keep up with the ever slowing
rate of rotation of the Earth. The last time a leap second had to be inserted was on 1th of January, 2017.

## Time zones

## Daylight Saving Time

## Updating time

## Calculating time

## Storing time

## Displaying time

[bkk-website]: https://bkk.hu/

[bkk-app]: /assets
