---
layout: post
title: Just Another Week - Netflix and Code
description: "some code and some netflix"
modified: 2014-04-06
tags: [netflix, code]
image:
comments: true
share: true  
---

This week went by relatively unprofoundly. I've spent most of my free time watching Netflix movies. 

- March 30: finished watching Arrested Development
- April 04: watched [Marc Maron: Thinky Pain](https://www.netflix.com/WiMovie/Marc%20Maron:%20Thinky%20Pain/70273401?trkid=438403)
- April 04: watched [Populaire](https://www.netflix.com/WiMovie/Populaire/70269481?trkid=438403)
- April 05: watched lots and lots of Archer
- April 06: watched [The Hairdresser](https://www.netflix.com/WiMovie/The%20Hairdresser/70132707?trkid=438403)

It's the week in which I've discovered my love for [dead pan comedy](http://en.wikipedia.org/wiki/Anthony_Jeselnik). 

### a bit of debuggin' ###

I've debugged something simple, but it was a bit of a "lesson learned" moment so I would tuck it in here. I was using SharedPreferences to save my TreeSet data, using TreeSet in order to keep things alphabetical (the data were of String types), when I noticed that upon retrieval, the data weren't... well, alphabetical.

{% highlight java %}
String [] values = {"T", "H", "I", "S"};
Set<String> set = new TreeSet<String>(Arrays.asList(values));
//the set.toString() at this point would be alphabetical
SharedPreferences settings = getSharedPreferences(SHARED_PREFERENCE_NAME, 0);
SharedPreferences.Editor editor = settings.edit();
editor.putStringSet(TREE_SET, set);
editor.commit();
//before 
set = settings.getStringSet(TREE_SET, new TreeSet<String>());
//the set.toString() at this point wouldn't be alphabetical
{% endhighlight %}

I was hemming and hawing about what was going on there, thinking that maybe I have somehow implemented the data structure incorrectly when I realized that, duh, the getStringSet() method returned a Set. Not a TreeSet. This solved that problem: 

{% highlight java %}
//after
set = new TreeSet<String>(settings.getStringSet("custom_irs", new TreeSet<String>()); 
{% endhighlight %}

And now everything works just fine. 

With one caveat: if the ordering of the element is dependent on when it was added to the Set, for instance, in a LinkedHashSet, than the element order would not be preserved. 

### what I'm listening to: ###

<iframe width="420" height="315" src="//www.youtube.com/embed/dV4_giHgDDk" frameborder="0" allowfullscreen></iframe>


