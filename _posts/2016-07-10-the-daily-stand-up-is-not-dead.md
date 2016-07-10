---
title: The daily stand-up is not dead
description: After switching to a Kanban system, our stand-ups have decreased in time and increased in efficiency.
---

The other day, Jan, one of my awesome colleagues, wrote [an interesting blog post on his vision of daily stand-ups](https://herebedragons.io/the-daily-standup-is-dead/). While I agree with him for the most part, there are a few things I have a slightly different opinion about. I also think the way we do stand-ups in the team I'm in is worth sharing. I wanted to reply with a comment to Jan's blog post, but because of [the finite amount of keystrokes I have left](http://keysleft.com/), I thought a blog post would be better than a comment.

## The same time each day

> First off, the same time each day thing. Every team that starts doing stand-ups does so at a designated time. But not everybody starts at the same time, neither might they be at the same location. People that start early will have to do a context switch and thus most likely lose productivity (between you and me, they will). If you need to be present from a distant location, this can also have an impact on the productivity of the stand-up, even in 2016. Technology is a bitch.

Our development team (Jan is in the app team, which is a separate team) is split up into three subteams: Ministry of Code, Fellowship of Code and Cabinet of Code. Every subteam has its own separate stand-up and they start at the same time every day. The Cabinet starts at 9:50, the Fellowship at 10:00 and the Ministry starts at 10:10.

The big advantage of starting at the same time is predictability, which makes it easier if you want to be a silent observer at another team's stand-up. If we at the Ministry are working on a feature that touches code that someone from another team has written in the past, that person can set a reminder and join our stand-up to see if there's something they can assist with. Or, if I know that I'll need to build on a feature currently in development at the Fellowship, I can join their stand-up to learn how things are going and what decisions are being made.

I don't believe the context switch has a negative impact on productivity, exactly *because* we always start at the same time. This way you can schedule your work a bit around the stand-up. Besides, in an office where NERF darts are almost eligible for frequent-flyer air miles, you learn to recover quickly from context switches.

## Development teams only

> Another annoying thing, but not directly related to this, is what is sometimes defined as a team that does a stand-up. Some companies tend to have stand-ups for development teams only. I don’t really see the point if you are closely working together on projects. You should know what’s going on, at least I do. If you have no idea what the guy next to you is doing, you have other problems. Stand-ups should be done with all those involved in a project. Talking to each other about code related issues is easy, the problems usually occur because of unclear or changing requirements.
> 
> The number 1 reason to go down the development-team-only road usually is that we assume the business side of things does not have time to participate or that they don’t care.

The Ministry, Fellowship and Cabinet stand-ups are all developer-only stand-ups, although everyone is free to join as a silent observer. A stand-up is basically a mini-meeting. That's why I like to handle stand-ups the way all meetings should be handled. Only people that actually *need* to be present should be present. There's no reason to have project leads, business leads, marketing members, copy members, customer care members and operations members present in every stand-up. If you need the entire project team, that's probably a sign the scope isn't suited for a stand-up. Book a separate meeting with a predefined agenda and a fixed start and end time. This will give everyone involved time to prepare which will make things more efficient.

## The way we do stand-ups

We started using a Kanban system in our development team a few months ago. After a few weeks we already started seeing benefits, which might be food for another blog post. Before we were using Kanban, our stand-ups were like Jan described them in his post: 15 people in a big circle and everyone got one minute to talk. Someone held up a timer so you could see your time ticking away. It even beeped at 30, 50, 55 and 60 seconds in. That really created some sort of pressure because when your minute was up, you had to stop talking, mid-sentence or not. As a result of the timer and the size of circle, you typically heard things like "Yesterday I worked on feature X, today they same". Not really valuable information.

### Use the board Luke
That all changed when we started using the Kanban system. The most important thing is our Kanban board. Everything starts from the board, even our stand-ups. Instead of talking about what we did yesterday and what we're going to do today, we talk about the state of the board. We go over each column, start downstream and work our way upstream.
 
* Any blockers in 'To launch'? No? Good! Yes? How could we help Operations? Let's go check after the stand-up.
* Hmm, that ticket has beens stuck in 'Testing' for four days now. Let's go check with QA after the stand-up to see what causing them problems.
* Is 'Ready for Testing' full? Yes it is. Is there anything further upstream that could move there but can't because the WIP limit is reached? Ok, no problem, we'll take that up with QA as well.
* Anything waiting for a code review? Ok, I'll handle that one.

When we get to the 'In progress' column (which means 'In progress' from a development viewpoint) we briefly go over what everyone is working on, check if the estimated due date is still realistic and discuss blockers or issues. If there are blockers or other issues, we take them up with the relevant person after the stand-up.

Finally we also have a glance at the 'Todo' column to see if there's anything that's more urgent than what we're working on now.

### Being late for a stand-up or working remote

If you can't make it to the stand-up, that's not really an issue since everything you need to know is perfectly visible on the board. We don't have fulltime remote workers, so we only need to cover for people working from home now and then. And, the same applies there, actually. The board tells you what you need to know and if necessary you can always give the rest of the team a short update on Slack.

### Not including people from other teams

This isn't causing us problems either because we know from the board and from our stand-up when to go to other project members. Besides that we also keep the project leads up to date in an informal way. That information ends up in more formal planning meetings and from there it trickles down to the relevant teams and/or team members. This isn't perfect yet, but it seems to be working pretty OK for now.

## Conclusion

I do agree with the general sentiment of Jan's blog post, but using Kanban and changing our stand-up accordingly has really been an eye-opener for me and changed the way I think about stand-ups. Our stand-ups have decreased in time and increased in efficiency. That's always a nice combination!

Oh, if you wan't become a member of the Ministry, the Fellowship or the Cabinet, have a look at [our jobs page](https://vikingco.com/en/jobs/). We're always on the lookout for new talent!