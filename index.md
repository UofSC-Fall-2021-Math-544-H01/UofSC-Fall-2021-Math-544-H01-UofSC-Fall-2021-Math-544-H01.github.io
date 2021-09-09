---
layout: home
title: Linear Algebra
nav_exclude: true
seo:
  type: Course
  name: Linear Algebra
---

# {{ site.tagline }}
{: .mb-2 }
{{ site.description }}
{: .fs-6 .fw-300 }

{% if site.announcements %}
{% assign announce_date = site.announcements.last.date | date: '%s' | plus: 604800 %}
{% assign today_date = 'now' | date: '%s' | times: 1 %}
{% if announce_date > today_date %}
{{ site.announcements.last }}
[Announcements](announcements.md){: .btn .btn-outline .fs-3 }
{% endif %}
{% endif %}

## Syllabus 

The syllabus can be found at the [about tab]({% link about.md %}). 

## Calendar 

At the [calendar tab]({% link calendar.md %}), you will find our topic schedule 
for each class along with the pre-reading, worksheets for that class, and 
due dates for assignments.  

## Notes 

The [notes tab]({% link notes/intro.md %}) is where you can find the course reading. 

## Homework and Worksheets

There are tabs for class [homework]({% link homework/index.md %}) and 
[worksheets]({% link worksheets/index.md %}). 

Homework is turned in weekly and in groups of 3-4. 

Worksheets are what we work in during class, also in groups. Worksheets are not 
turned in - you are only graded on how much you present solutions to them. 

For more information, see the [Syllabus]({% link about.md %}).

## Weekly schedule 

If you ever need to remind yourself about the time and coordinates of our course or 
my office hours, you can quickly reference at the [schedule tab]({% link schedule.md %}).

## Me

If you are interested in a bit about who I am and what I do, check out the 
[staff tab]({% link staff.md %}) or visit [my website](https://www.matthewrobertballard.com).
