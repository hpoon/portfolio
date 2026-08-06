---
layout: post
title: "UBC Engineering Competition 2011"
categories:
  - Engineering
  - Robotics
  - Competition
image: assets/images/cropped-IMG_0082.jpg
description: "Autonomous vehicle competition using Vex Robotics to repair solar panels and underwater transmission lines"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2011/11/06/ubc-engineering-competition-2011/](https://blog.henrypoon.com/blog/2011/11/06/ubc-engineering-competition-2011/)

Just like last year, I participated in the UBC Engineering Competition again, except this time, I competed with a different team. Although the winning team would have a chance to compete in the next level of competition (I don't even know where that would be – last year it was in Saskatoon), two of our teammates couldn't make it even if we won. One of them would be flying to Hong Kong and another was starting a Co-op work term in the Silicon Valley working for NVidia. It didn't matter though, because we didn't win first place this year.

This year's competition problem involved the following scenario: normally solar panels are able to rotate toward the sun, but sometimes they get stuck, therefore it requires people to go out there and rotate them manually. Also, undersea transmission lines sometimes get severed and also require manual repairs. Our task was to build an autonomous vehicle using a VeX Robotics Kit in about 5 hours to use in a small scale arena emulating similar conditions. A wooden pole represented the solar panel, that we had to rotate and a plastic pipe represented the transmission line. To "repair" the transmission line, we had to build a repair module using newspaper and popsicle sticks that could physically cover up the pipe. Additionally, in order to reach the transmission line, the vehicle would have to cross a rice field (represented by uncooked rice) and cross a river (ensuring that no electronics get damaged, they had to be above the "water line" at all times – represented by the dip in the arena). After designing our vehicle, we would also have to present our design to the judges.

When I heard what the problem was, I thought to myself, "this is an impossible problem given the time we have to build it and lots of teams aren't going to be able to perform the task". I guess it was supposed to be like that. The problem couldn't be too easy or otherwise everyone would be able to do it. Despite the difficult task, we approached it with a super chill attitude throughout the entire competition.

As a group, we planned out what we wanted to do. We thought that it would be straightforward to go across the river, but it turned out that it wasn't that straightforward. We had trouble keeping our electronics above the "water". The line follower kit we used could follow the black line quite accurately, but it had to be about an inch above the ground.

To make matters worse, the wheels kept falling out. Normally, one should just have to insert the shaft into the motor clutch and connect the clutch to the motor, but the connection was quite loose.

![]({{ site.baseurl }}/assets/images/IMG_0062.webp)

One of our teammates spent about 3 and a half hours trying to fix the wheels and he succeeded. It took up a lot of time that we needed for the other design tasks, but we couldn't leave that alone since movement along the ground was a critical function.

![]({{ site.baseurl }}/assets/images/IMG_0056.webp)

In the meantime, we brainstormed how we would rotate the vehicle to face different directions when needed, how we would pick up the repair module, and how we would rotate the solar panel, and how to protect the line followers while crossing the river. We also had to think of what we were going to say for the presentation.

We couldn't really get the rotation to be accurate without using an encoder (which would increase our product cost), so we tried to see what we could do without being able to rotate the vehicle. We could drive straight toward the solar panel, rotate it, and return to the base. If we focused on just this task, we didn't have to figure out how to figure out the other tasks. We figured that most teams wouldn't be able to perform that task anyway. With that in mind we modified our design drastically and came up with something that kind of worked.

![]({{ site.baseurl }}/assets/images/IMG_0065.webp)

The end reached high enough such that we could just bump into the top of the solar panel and rotate it and then go back to the base. We didn't need to worry about the other task of repairing the underwater transmission line. There wasn't enough time for that.

When it came to the presentation, we talked about our design and answered the questions quite well, but one of the competitors asked us a question that a lot of people seemed to feel was a very jerk question to ask. He asked "how would the client feel that we delivered a product that could not meet all the stated requirements?" I guess he was bitter that my team beat his team last year and felt threatened by me this time around. We answered the question by saying that it's better to do one task well, than to fail at both.

In the competition, a lot of teams did in fact fail the tasks and did absolutely nothing. When it came time for our device to compete, we did what we could. It did reach the solar panel and rotate it a bit, but not enough to rotate it all the way. It couldn't even complete one task, although we had tested it before and saw that it did work.

The winning team (the same team as the guy who asked us that terrible question), used a design that would travel align the walls, past the river and to the broken line. It picked up the repair module (shaped like a table) using a flat pad to slide underneath to pick it up. It managed to do a 90 degree turn by following the wall (push sensors would tell the vehicle that it had in fact touched a wall). It was clear that their design won out over everyone else's, and they totally deserved the win.

![]({{ site.baseurl }}/assets/images/IMG_0074.webp)
