---
layout: post
title: Diving into MTA Turnstile Data - Project 1
---
The  Beginning:

The New York City Transit Authority provides a vast amount of information regarding each subway station in NYC. It provides data from each turnstile at each station every four hours. We are able to extract the number of entries from each station. 

This leads us to my first project at METIS. "Women Tech Women Yes" (WTWY) is hosting a gala at the begining of summer. They want to find out where they can effectively place their street team to hand out invitations to ge the best response rate. The more people invited the more awareness they build about WTWY. 

To approach this problem, we first wanted to understand the data provided by the MTA turnstile. After looking at the .csv file provided by them we know that there's a number of "Entries" for each turnstile at each station. Each station has multiple turnstiles. The number for entries doesn't represent the actual number of entries, but rather its a continuous count. Therefore in order to extract the actual number of entries, we must subtract the previous entry number from the new entry number. 

Our group decided that since the gala is duting the summer, we would want to send out the invitations at least two to four weeks ahead of time so that people have time to RSVP to the event. We looked at the time points between 5/18/2019 and 6/06/2019. 

Our group decided that we would look at traffic through each station and determine which stations have the most traffic. From there we would focus on stations where there are more Tech companies and narrow down our list. In order to determine which stations have the most foot traffic we have to calculate the amount of peolpe going through each station. We did this by creating a new column which listed the entries number from the previous date. We then subtracted the date from the previous date to get the actual number of entries and not some arbitrary count. We then tallied all the number of entries from each turnstile for each stations and obtained the stations with the most entries. 

The top 10 stations that we obtained from our data indicated these as our top stations:

1. 34 St Penn Station
2. Grand Central 42 St
3. 34 St Herald Sq
4. 23 St
5. 42 St Port Auth
6. Time Sq 42 St
7. World Trade Center
8. 14 St Union Sq

![Top 20 Stations]({{sodas32.github.io}}/images/top20bar.png)

We wanted to be sure that our data made sense so we double checked with the official MTA data to see if our stations are somewhat similar to the official data. The MTA's official most active stations are: 

1. Time Sq 42 St
2. Grand Central 42 St
3. 34 St Herald Sq
4. 14 St Union Sq
5. 34 St Penn Station

The top five stations from the MTA's official data falls within our top eight stations. This gave us a sanity check to make sure our data wasn't really skewed or wrong. 

Now that we have a list of stations with the most traffic in those dates, we decided to focus more on which stations are around more tech companies. After a brief google search we found that there are a few clusters of tech companies in Manhattan. We decided to focus more on 14th St Station as large tech companies such as Google, Amazon, Compass...etc are located around there. 

Our focus now shifted to looking deeper into 14th St Station. We decided to look more into which days of the week are better for placing street workers. We split the data into days of the week over the 3 week span and found that more people ride the subway on weekdays and there is a dip in ridership during the weekends. This makes sense as people will be commuting more during the weekdays than weekends. 

The conclusion we came to, and suggestion to WTWY, is that they place their workers near 14st Station during weekdays. This would give them a higher chance of meeting someone in tech that will attend their event. 

If we wanted to further advance our model, we could investigate during what time do people enter the stations. Are mornings better than afternoons/night? This will allow them to place street workers at the appropreiate time 



```
---
layout: post
title: Zach's Test Post
---
```


markdown-y things.


[This is a link](http://thisismetis.com)

![Image test]({{ site.url }}/images/AlanLeeShireGandalf.JPG)

### Other things
* Like
* lists
* and 
* stuff
