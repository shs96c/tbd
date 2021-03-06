---
date: 2017-01-05T09:42:02+05:00
title: Five Minute Overview
weight: 10
---

## Distance

{{< quote title="Branches create distance between developers and we do not want that" >}}
&mdash; Frank Compagner, Guerrilla Games
{{< /quote >}}

Assuming any network accessible source control, physical distance is mitigated by AV technologies including 
screen sharing. So we will not worry about that so much these days.

Frank's 'distance' is about the distance to the integration of code from multiple components/modules/sub-teams for a 
binary that could be deployed or shipped. The problematic distance is to code not yet in the single shared branch, 
that might:

* break something unexpected once merged
* be difficult to merge in.
* not show that work was duplicated until it is merged
* not show problems of incompatibility/undesirability that does not break the build

Trunk Based Development is a branching model that reduces the distance to the max. 
 
## What it is

{{< note title="Notes" >}}
* Use of "Developers" throughout this site, means "QA-automators" for the same buildable thing, too.
* When we say 'the trunk' on this site, it is just a branch in a single repository that developers in a team are focusing on 
for development. It may be called 'master'. That hints at the fact that the branch in question may literally not be 
called 'trunk' at all.
{{< /note >}}

There are many deciding factors, before a development team settles on Trunk Based Development, but here is a short overview 
of the practices if they do:

### Releasability of work in progress

Trunk Based Development will always be **release ready**

If an executive manager visited the development team and commanded "Competitor X has launched feature Y, go 
live now with what we have", the worst response would be "give us one hour". The development team might have been very 
busy with tricky or even time consuming tasks (therefore partially complete), but in an hour, they are able to go live 
with something just stabilized from the trunk. Perhaps they can do it in less than, an hour. The rule though, is never break 
the build, and always be ready for that CIO-commanded disruption to plans.

#### Where releases happen

A key facilitating rule here is that Trunk Based Development teams exclusively **either** release directly from the 
trunk - see [release from trunk](/release-from-trunk/), **or** they make a branch from the trunk for the specifically for 
the actually releasing. See [Branch for release](/branch-for-release/).
Teams with a higher release cadence do the former, and those with a lower release cadence to the latter. 

### Checking out / cloning

All developers in a team that work on a application/service, clone and checkout from the trunk. They will 
update/pull/sync from that branch a many times a day, knowing that the build within it works perfectly. Their fast 
source-control system means that their delays are a matter of a few seconds for this operation. They are now 
integrating their team-mates commits on an hour by hour basis.

### Committing

Similarly, developers completing a piece of development work (changes to source code), that provably does not 
break the build, will commit it back to the trunk. The granularity of that commit (how many a developer 
would implicitly do a day) can vary, and is learned through experience, but commits are typically small.

The developer needs to run the build, to prove that they did not break anything with the commit **before** the commit
is pushed anywhere. They might have to do a update/pull/sync before they commit/push the changes back to the team's 
version control server, and additional builds too. There's a risk a race condition there, but lets assume that is not 
going to happen for most teams.

### Code Reviews

The developer needs to get the commit reviewed. Some teams will count the fact that the code was developed according 
to pair programming as an automatic review. Others team will follow a conventional design where the commit is marshaled
for review before landing in the trunk. In modern portal solutions, marshaled nearly always means a branch/fork (Pull
Request) that is visible to the team.

![](/images/trunk_pr.png)

^ the speech bubbles are stylized code review comments

Code review branches can (and should) be 
deleted after the code review is complete, and be very short lived. This is tricky for teams new to Trunk Based 
Development. 

Noe: You want to keep 
the commentary/approval/rejection that is part of the review for historical and auditing purposes, but you do not want to 
keep the branch. Specifically, you do not want to developers to focus on the branch after the review.

## A safety net

[Continuous Integration](/continuous-integration/) (CI) daemons are setup to watch the trunk (and the short lives feature 
branches used in review), and as quickly and completely as possible loudly/visibly inform the team that the trunk
 is broken.  Some teams will lock the trunk, and roll-back changes. Others will allow the CI server to do that 
 automatically.

![](/images/5trunk1.png)

The high bar is verifying the commit before it lands in the trunk. Short lived Pull Request branches are the modern
place for that.
 
## Developer team commitments

As stated, developers are pledging to be rigorous and not break the build. They're also going to need to consider 
the impact of their potentially larger commits, especially where renames or moves were wholesale, and adopt techniques
to allow those changes to be more easily consumed by team mates.

## Drilling into 'Distance'

Problematic 'distance' has a few tangible examples:

* Late merges of development that happened more than a couple of days ago.
  * Difficult merges in particularly
* A breaking build that lowers development team throughput, and diverts resources while it is being fixed

# References elsewhere

<a id="showHideRefs" href="javascript:toggleRefs();">show references</a>

Date    | Type  | Article
--------|-------|--------
16 Jun 2015 | Blog Entry | [Organization Pattern: Trunk Based Development](http://www.alwaysagileconsulting.com/articles/organisation-pattern-trunk-based-development/)


