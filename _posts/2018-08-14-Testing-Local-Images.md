---
layout: post
title: Diving into MTA Turnstile Data - Project 1
---

The New York City Transit Authority provides a vast amount of information regarding each subway station in NYC. It provides data from each turnstile at each station every four hours. We are able to extract the number of entries from each station. 

This leads us to my first project at METIS. "Women Tech Women Yes" (WTWY) is hosting a gala at the begining of summer. They want to find out where they can effectively place their street team to hand out invitations to ge the best response rate. The more people invited the more awareness they build about WTWY. 

To approach this problem, we first wanted to understand the data provided by the MTA turnstile. After looking at the .csv file provided by them we know that there's a number of "Entries" for each turnstile at each station. Each station has multiple turnstiles. The number for entries doesn't represent the actual number of entries, but rather its a continuous count. Therefore in order to extract the actual number of entries, we must subtract the previous entry number from the new entry number. 

Our group decided that since the gala is duting the summer, we would want to send out the invitations at least two to four weeks ahead of time so that people have time to RSVP to the event. We looked at the time points between 5/18/2019 and 6/06/2019. 


```
---
layout: post
title: Zach's Test Post
---
```

Part in the post to tell the page how to title your post and how to render it.

Below are some examples of loading images, making links, and doing other
markdown-y things.


[This is a link](http://thisismetis.com)

![Image test]({{ site.url }}/images/AlanLeeShireGandalf.JPG)

### Other things
* Like
* lists
* and 
* stuff
