---
title: Building a Skill for Claude, Twice
description: One system taught me the pattern. The other one tested whether I understood it.
date: 2026-07-08
tags:
  - ai
  - claude
  - softwaredevelopment
  - architecture
  - tools
layout: layouts/post.njk
---

I built the same kind of thing twice this year: a "skill," a small set of markdown files that tell Claude how to operate inside a specific codebase instead of getting re-explained from scratch every session. The first was for my team at Summit. The second was for my own job search. From the outside they look almost identical. The second one is the one that actually taught me something.

## What a skill actually is

If you haven't used Claude Skills yet, the idea is simple. Instead of pasting a wall of context into every conversation, or hoping a model remembers what it learned last week, you write small, focused files that describe what they cover and when to load them. A session reads an index first, decides which files are actually relevant to the task in front of it, and only pulls in those. The rest stays on disk until something triggers it.

That "on demand" part matters more than it sounds like it should. The failure mode without it isn't "the assistant doesn't know enough." It's the opposite: everything gets loaded every time, the useful signal drowns in a wall of context nobody asked about this session, and you end up paying for and reading through six repos worth of documentation to answer a question about one function.

## Version one: stop being the bottleneck

At Summit I'm the person who's held most of the "how does this actually work" knowledge across a dozen repos spanning three tech generations: legacy Java monoliths, a current Vue 3 / Nuxt frontend, and a layer of Node Lambdas holding it together. That's a fine way to be useful and a bad way to run a team. Every new developer, every PR review, every "wait, why does that break" question routed through me, whether or not the answer actually required me specifically.

So I built a skill index. The shape ended up being:

- **Core skills** split by concern: what repos exist and what runs where, the security landmines nobody should touch without asking first, how the applications actually talk to each other, how a deploy actually happens, who owns what.
- **Workflow skills** for the recurring rituals: how to review a PR end to end, what to do at the start and end of a working session, how documentation gets updated.
- **A profile per developer**, because "how do I run this locally" has a different answer on every laptop, and that answer shouldn't have to live in my head either.

A skill entry looks roughly like this:

```
### skills/core/deploy.md
**Load when:** preparing a release, investigating a failed deploy,
or any question about the CI pipeline.
**Covers:** deploy gate rules, environment promotion, smoke tests.
```

Small, boring, and exactly as long as it needs to be. The part that made it actually trustworthy wasn't the structure though, it was the update discipline. New information gets appended, never silently overwritten. Corrections get annotated with a date instead of just replacing the old line. Each change to a skill file is its own small commit. That sounds like a lot of ceremony for a markdown file, but it's the difference between a skill system the team trusts and a wiki everyone quietly assumes is out of date.

The point of the whole exercise was to stop being the only one who understood the system, not to document the current state of me being that person forever. A skill file that only I can update isn't actually a fix.

## Version two: the same idea, much higher stakes

Then I tried to build the same kind of system for something with a completely different threat model: my own job search.

The problem shape was familiar. A job search run as a long collaboration with an assistant, across many sessions, breaks in specific ways if nothing accounts for them. Every new session starts from zero unless something tells it what's already been decided. Resume bullets get a little rounder every time they're rewritten, "owned and operated a platform" drifts toward "architected a platform" a sentence at a time, and nothing catches that unless something is specifically designated to catch it. A single positioning strategy doesn't fit every role either; a resume that leads with leadership reads as exactly wrong for a role screening for a senior IC.

None of that was new to me. I'd more or less already learned it building the Summit skill. What's different is the last item on the list: personal data doesn't belong anywhere near a system you might eventually want to show off. A salary floor and a recruiter's phone number can't sit in the same directory as something you'd hand to a stranger as an example.

At Summit, being a little loose about what counted as sensitive mostly cost me an awkward Slack message. Here, being loose about it means a real number sitting in a directory that might eventually get pushed public. That's not a bigger version of the same problem. It's a different problem that happens to rhyme with the first one, and it needed a different answer: not just a convention about what goes where, but a way to check the convention actually held.

The shape that came out of it is a three-layer split. A `framework/` layer is the reusable system: no personal data, works for anyone, could be handed to a stranger. A `private/` layer is the actual data, and it's not just gitignored, it's its own independent git repository nested inside a path the outer repo never sees, so a real job search still gets real version history without any of it entering a public commit log. An `output/` layer holds generated deliverables, gitignored, disposable. The test for where a sentence belongs: would it still make sense if `private/` were deleted? If a methodology file has to say "the candidate's floor" instead of an actual dollar figure, it's in the right layer. If it says the number, it's in the wrong one.

## Where it actually went wrong

I got the boundary wrong once while building it, which is exactly the kind of thing worth writing down honestly instead of only presenting the finished version. An early draft of the public entry-point file had my actual comp floor and actual excluded relocation regions typed directly into it, before the config-separation pattern existed to prevent that. It was never committed. It still existed, uncommitted, sitting in a directory that would eventually be pushed public. The fix wasn't just deleting the numbers. It was building a small config file to hold them, rewriting the file to reference it instead of restating it, and then grepping every public-facing file for personal identifiers before I let myself trust the boundary at all.

The second mistake was quieter. Earlier reasoning had deliberately decided a Staff/Principal IC resume should lead with technical impact rather than leadership, specifically so a reviewer wouldn't misread a leadership-forward opening as an EM candidate instead of a senior IC. Later, while extending that same resume to a second page, the section got reordered to lead with leadership anyway, justified by perfectly reasonable general advice about not burying your best material. The advice was correct on its own. It just silently reversed an earlier, more specific decision, and I only caught it because I checked an actual transcript instead of trusting my own summary of what I'd already decided.

Both mistakes point at the same fix: when something might contradict an earlier decision, check the record, not a summary of it, even a summary you wrote yourself.

## The actual lesson

The second skill system didn't need a fancier pattern than the first one. It needed the same pattern, an index loaded first, small files loaded on demand, append-only updates, a boundary between what's generic and what's specific, except this time the boundary needed an explicit check instead of a habit I trusted myself to remember. The team version taught me the shape. The personal one taught me that the shape doesn't protect you by existing. It protects you when you build in a way to catch yourself breaking it.
