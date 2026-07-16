---
title: Building a Claude Skill Repo That Survives Routine Use
description: A skill is easy to write. Keeping a repository of them trustworthy past the first month is the part nobody warns you about.
date: 2026-07-16
tags:
  - ai
  - claude
  - softwaredevelopment
  - architecture
  - tools
layout: layouts/post.njk
---

A Claude skill is easy to build. Keeping a repository of them useful past the first month is the part nobody warns you about.

I've built two of these now. One for my team, so the codebase knowledge that had collected in my head could live somewhere the rest of the team could actually reach. One for myself, running a long project across dozens of sessions. Different subjects, same shape, and the same failure modes turned up in both. This post is about that shape, and more to the point, about the maintenance habits that decide whether the thing is still worth trusting in week six.

## What a Claude skill actually is

If you haven't used Claude Skills yet, the idea is small. Instead of pasting a wall of context into every conversation, or hoping the model remembers what it picked up last week, you write short markdown files that each cover one concern: what they're about, and when they're worth loading. A session reads an index first, decides which files are relevant to the task in front of it, and pulls in only those. Everything else stays on disk until something calls for it.

That "on demand" part carries more weight than it looks like it should. The failure mode without it isn't that the assistant knows too little. It's the reverse. Everything loads every time, the one paragraph that mattered drowns under five repos of documentation nobody asked about this session, and you spend context and attention reading all of it to answer a question about one function. A skill file earns its place by staying quiet until it's actually needed.

## Why a repository, and not just a folder of notes

You could keep these files anywhere. Putting them in a real repository, under version control, is what turns them from personal notes into something a team can lean on.

On my team I was the person holding most of the "how does this actually work" knowledge across a dozen repos and three generations of tech. That's a useful thing to be and a poor way to run a team. Every new hire, every review, every "wait, why does that break" routed through me, whether or not the answer needed me specifically. A skill repo was the way out, but only because it was a repo. A skill file that lives on my laptop, or that only I ever update, just documents the bottleneck instead of removing it.

The version control isn't decoration. New information gets appended, not silently overwritten. A correction gets a dated note instead of quietly replacing the old line. Each change is its own small commit. That's more ceremony than a markdown file seems to deserve, right up until you notice it's the whole difference between a skill system a team trusts and a wiki everyone assumes is out of date. The history is the reason a reader believes the file.

## The shape is the easy part

Here's the uncomfortable thing the second repo taught me: the shape didn't need to be any fancier than the first. Index loaded first, small files on demand, disciplined updates. That pattern was never the hard part. The hard part is that the pattern doesn't protect you by existing. It protects you when you build in a way to catch yourself breaking it. Most of what's below is those catches, and most of them I only added after something slipped.

### Give every skill a header budget

Discovery stays cheap only while the index stays cheap to scan. The rule that made this work: every skill states what it covers and when to load it in a fixed handful of lines at the very top, short enough that a single pass reads all of them at once. The budget does a second job too. When a header won't fit, that's almost always a sign the skill is trying to cover two concerns and wants splitting. A routing header that sprawls is a routing system that has quietly stopped routing.

### Build the routines in pairs

A repo used across many sessions needs a start and an end. The opening routine reads the current state before doing anything. The closing routine writes it back. They only work as a pair. If the close slips, tomorrow's open reads yesterday's stale notes and trusts them completely.

The trap is that the real work of a session, the actual review or the actual draft, crowds out the bookkeeping, which gets pushed to "later" and sometimes never comes. So the bookkeeping has to be cheap and close to automatic. Log events the moment they happen rather than reconstructing them at the end. Generate the readable views instead of hand-maintaining them. Fold the day into a single commit so the history stays legible. A routine you have to remember is a routine you'll skip on the day you're busy, which is the day it mattered.

### Generate your views, never mirror them

This one earned its spot by breaking first. If the same information lives in two files that are both edited by hand, they will eventually disagree, and you won't notice until one of them lies to you. Anything readable that restates structured data, a summary or a status list or an index, should be generated from a single source rather than kept in step by willpower. Willpower is exactly the thing that runs out at six on a Friday.

### Watch for the system describing itself in too many places

A repo like this ends up describing itself: a couple of readmes, a directory tree or two, a setup script, the session map that gets read first. Every one of those is a mirror of the real structure, and mirrors drift. You change the layout, most of the descriptions get updated, and one or two quietly start lying.

The habit that helps is a single "when you change X, also touch Y" map, kept in one place, so the ripple of a structural change is written down once instead of rediscovered every time.

But the more interesting failure lives here, and it's worth being honest about because I hit it recently. Having the map isn't enough. I made a small structural change, updated most of the mirrors, and missed a couple. The map that would have told me had existed the whole time. I just didn't open it, because the change came up in the middle of a session and my routine only consulted the map at the start. The map was fine. The timing was the problem.

The fix wasn't a better map. It was making the map turn up where I'd actually see it. The opening routine now regenerates that "what to touch when" reference every session and drops it into the working scratch space, built from the real sources rather than hand-copied, so it can't fall out of date. The file isn't the point. The point is that the guidance is sitting in front of me at the moment I'm about to need it, instead of waiting politely in a document I've stopped opening.

### Keep the sensitive things in one place, and check that you did

My two repos had very different stakes here. The team one held nothing worse than internal detail. The personal one held things I'd never want in a public commit, and it was also the one I might eventually want to show people. Those two facts pull in opposite directions.

The answer was to separate the sensitive values from the prose that uses them, the same way any project keeps secrets out of its code. One config file holds the specifics. The methodology files refer to them by name, never by value. The test for whether a sentence is in the right place: would it still make sense if the private data were deleted? If a file has to say "the candidate's floor" rather than an actual number, it's in the right layer. If it states the number, it isn't.

I got that boundary wrong once, which is the part actually worth writing down. An early version of the public entry-point file had specifics typed straight into it, before the config split existed to prevent that. It was never committed, but there it sat, in a folder headed for public. Deleting the values wasn't the fix. The fix was building the config file to hold them, rewriting the prose to reference it, and then grepping every public file for those specifics before I let myself trust the boundary at all. A convention I'd trusted myself to remember had already failed once. A check hadn't.

## The actual lesson

Both repos taught the same thing from opposite ends. The shape of a skill system is genuinely simple, and you can have the whole thing sketched in an afternoon. What decides whether it's still worth anything a month later isn't the shape. It's whether the routine that keeps it honest is cheaper than the shortcut that lets it rot, and whether the checks that catch your mistakes run without you having to remember to run them.

So write the small files, and put them in a repo. Then spend most of your effort on the part that isn't the files: the header budget that keeps discovery cheap, the routines that read and write state as a pair, the views you generate instead of maintain, the ripple guidance that shows up on its own when you need it, and the boundary you verify instead of trust. The pattern is the easy part. The habits around it are the actual product.
