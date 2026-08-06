---
layout: post
title: "UBC Engineering Competition 2010"
categories:
  - Engineering
  - Robotics
  - Competition
image: assets/images/cropped-firstprotocollision.jpg
description: "First place win at UBC Engineering Competition with an autonomous vehicle using Vex Robotics"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2010/11/13/ubc-engineering-competition-2010/](https://blog.henrypoon.com/blog/2010/11/13/ubc-engineering-competition-2010/)

A couple weeks ago, a classmate of mine invited me to participate in the UBC Engineering Competition in Senior Design. After checking the calendar to see if I was free that day, I accepted. I later found out that the winners of this competition would represent UBC in the Western Engineering Competition in Saskatoon, which will take place in January. The problem with this was that three out of the four people on my team had a Co-op work term (myself included). Despite the fact that we knew we weren't going to the competition, we went to compete anyway. There was little pressure for us, and winning or losing didn't matter.

Some time later, I realized that my friend's birthday party was the day before the competition, which meant I probably wasn't going to get a lot of sleep. Indeed I was right. I got home at about 2:30 in the morning and had to arrive at the competition at 8:30. Before I slept, I read an email that told us to read over the competition materials and to prepare a PowerPoint presentation template for the competition. Seeing that we weren't aiming to win the competition, I neglected to do any of this preparation. My teammates neglected this as well.

On the morning of the competition, we went through all the registration procedures and find out what the design problem was. Our task was to build an autonomous vehicle that could transport an object and bring it back to the starting location. The only parts we were given was the Vex Robotics Kit, which came with a microcontroller, motors, wheels, and parts to build the frame. We would be scored on how many objects we picked up, the weight of the vehicle, and the team's presentation performance.

![]({{ site.baseurl }}/assets/images/arena.jpg)
*The Arena. Each team's vehicle drives off the big ramp to pick up only the gray objects and not the black foam blocks. A large white hula hoop surrounds the field.*

Since we didn't really aim to win the competition, the team ended up being super chill through the entire competition. One of the officials said to us, "Your team is the least stressful team we've seen!" We made so many lame/funny/stupid jokes during the competition and had such great laughs. Throughout the entire competition, I was probably super sleepy, and found no time to rest at all. Despite the fact that we didn't aim to win, we still tried hard in the competition.

Our strategy was simple: KISS. Keep It Simple Stupid. We realized that in the 5 hours we were given to design it, we did not have time to make anything complex. It made the most sense.

The biggest design issue was the question of how the vehicle was going to know how to return back to its starting location after it leaves. The only sensors we were given were buttons that would be pressed when the vehicle ran into an object. None of these sensors would help us achieve this. We thought of making the robot do a 180 degree turn, but this was difficult since we didn't really have a way of measuring how many degrees the vehicle had turned. We tried to time it, but the time it took to turn varied depending on how heavy the cargo was. One of my teammates came up with the terrific idea of not rotating at all. The vehicle would drive straight, pick up and then go in reverse back to the starting location. We would then orient the vehicle in another direction to pick up the next object (we were allowed to do this since teams are allowed to touch their vehicle when it is in the starting location).

Our first prototype followed a simple strategy: run into an object, do a 180 turn, and bring it back.

![]({{ site.baseurl }}/assets/images/firstproto.jpg)
*First Prototype. Run into an object, do a 180 turn, bring it back.*

We quickly found that the 180 degree turn was difficult to implement reliably. Our second prototype used the same methodology but added sensors at the front to know whether it had reached the boundary of the arena or not.

![]({{ site.baseurl }}/assets/images/secondproto.jpg)
*Second Prototype. Same methodology still, but now has added sensors at the front to know whether it has reached the boundary of the arena or not.*

Going with our final strategy, the vehicle would drive in a straight line toward the target object. A sensor placed in the front of the object would be activated when the vehicle hit the object. This would signal a cage to come down and enclose the object. Then the vehicle would go in reverse back to its starting location. The cage was simply a "fence" that was initially raised and then lowered to enclose the object.

![]({{ site.baseurl }}/assets/images/thirdproto1.jpg)
*Third Prototype. Seeing how the 180 rotation didn't really work, we decided on the cage idea. Run into an object, close the gate, and reverse back to base. Winning strategy right there.*

After a lot of testing, we were quite confident that ours was going to work. While doing all of this testing and designing, one of my group members made the PowerPoint presentation. It basically talked about how the device worked and our design strategy.

The only preparation for the presentation that we had was just 5 minutes of telling who would present which slide. When it came time for us to present, we looked at the slide and pretty much made up what we were going to say on the spot. Because of this, our presentation seemed quite natural. The fact that we all worked on the project allowed us to all know what we were talking about, so we didn't stutter a lot. I figure we did okay on the presentations. Nothing spectacular.

After the presentations, each team took turns demonstrating their device. There were a few designs that were definitely innovative, ambitious, and simple. Among these, there was one that lowered a large arm onto the ground and sweep in a 360 to catch all the objects and return them all home at the same time. It was a interesting design, but there was no way for the robot could do a perfect 360, since it was impossible to get the timing for it right and the power the motors gave would not be enough to move the entire load. There was also a design that relied on randomly searching the entire field for an object and then moving around the perimeter of the field to return home. This was the most ambitious design, but it didn't work out because its random searching didn't find any objects to grab. Another team relied on the same principle as ours but were heavier.

As each team demonstrated their vehicle, it became apparent that our team had a big chance of winning. We were very confident that we would get at at least one object, and our vehicle was the lightest one. The team with the lightest vehicle would score the most points in terms of weight. But for object retrieval, no team retrieved more than one object. It was either one or zero. If our vehicle grabbed even one object, we would be in first place for vehicle performance. When it became our team's turn to demo, our vehicle worked exactly the way we wanted it to. We grabbed one. We went on the grab another, but due to us failing to aim the vehicle properly, we failed to grab a second. But it didn't matter, we were in the lead in points. Since no team grabbed more than one, we placed first in terms of vehicle performance. We had a chance to win.

After the officials calculated the totals of all the scores, my team placed first out of twelve teams! The best part about this is that even though we did zero preparation, we came out on top because we executed our design strategy better than the other teams. We made use of the testing time to make sure our project actually worked. It seemed like a lot of the projects weren't tested that thoroughly, but that might have to do with the intense time pressure and a complex design. The lack of pressure to win allowed us to perform so much better.
