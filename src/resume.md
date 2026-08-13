---
layout: layouts/resume.njk
title: My Resume
tags:
  - nav
  - me
navtitle: Resume
templateClass: tmpl-resume
---

**Staff / Principal Software Engineer**
*Technical Direction | Distributed Data Infrastructure | Legacy Modernization*

Twelve years setting technical direction from inside the code, usually as the person a platform can't run without. I carry a working model of the whole system, which is how I spot where a change will break something three steps away, and I write that knowledge down so it stops depending on me. My depth is in distributed data infrastructure, AWS, and legacy modernization. I own critical production systems and grow the engineers around me.

**Core competencies:** Distributed Systems | AWS Operations | Software Architecture | Platform Engineering | Event-Driven Architecture | Legacy Modernization | Production Reliability | Technical Mentorship

##  Experience

### Lead Developer - Summit Professional Education
Dec 2021 - Present

*Senior-most engineer and technical owner for a platform serving 528K accounts, 3.5M+ enrollments, and ~20K monthly active professionals across all 50 states. Full-time through Aug 2026, retained since as an independent architecture advisor on in-flight platform and billing migrations. (Staff Engineer / Engineering Lead scope)*

+ Set direction to retire a legacy Universe/Pick data-entry system by building its replacement Vue 3-native on the next-generation ops platform, turning a framework migration the board wouldn't fund into a side effect of new feature work.
+ Cut a customer-facing B2B account page from ~10 minutes to under a minute with a relation-table redesign; the sales team had refused to demo it and now uses it live to close contracts.
+ Owned the subscription engine at the center of the platform: Recurly subscriptions mirrored through webhooks into a near-real-time access-grant cache in Aurora, processing roughly 60K paid subscription invoices a year.
+ Eliminated 12+ monthly dev tickets by making B2B client signup pages, negotiated-discount groupings, and account rosters sales-configurable.
+ Operated as the team's safety net instead of its bottleneck: I handed off clean problem definitions so three of five engineers ran their own domains, the website, the Yeti platform, and the deployment pipelines, end to end, while I owned every code review and pull request.
+ Served as the sole technical partner to a non-technical CTO brought in during a 2024 leadership change, his only direct report, translating system realities into decisions he could act on.
+ Championed AI-assisted development from zero, bringing JetBrains AI Assistant to every engineer, then decomposed a CTO's single-file prototype into an on-demand skill system with per-developer profiles, a PR-review workflow, and a repository wiring map, so cross-system knowledge lives in the repo.
+ Coached engineers through migrations they wouldn't attempt alone, including a nine-month Vue 2 to Vue 3 migration where I asked questions and let the engineer make the architectural calls.
+ Mentored a bootcamp-trained frontend developer who grew into a full-stack contributor and now owns the deployment pipeline for the main website and its API, releasing directly to both test and production.
+ Recovered a week of failed payments caused by a finance-side processor change, scripting bulk retries against Recurly's API and pivoting from Python to Node around a blocking bug in the official client library.
+ Implemented new AWS Personalize, AWS CloudSearch, and Pipedrive integrations, and maintained and evolved the platform's broader integration surface spanning Recurly, Iterable, ON24, HubSpot, and Podbean.
+ Recovered organic search from ~30th to a consistent top 10 after an SSR regression, directing a specialist's fixes across ~300 server errors and 600+ Core Web Vitals issues.
+ Shipped a board-mandated CMS migration abandoned mid-flight, landing static HubSpot pages alongside the Nuxt app with no visible seam to users.
+ Maintained 140+ Lambda functions across the auth path and core business workflows at near-100% measured availability, and led the AL2 to AL2023 migration with a clean-environment strategy.
+ Aligned product, marketing, sales, and customer service behind a single engineering priority queue, turning four departments' competing demands into clean execution on every new product and feature.

### Software Engineer - Juice Plus
Jun 2020 - Dec 2021

+ Took sole ownership of an undocumented, business-critical Java ETL and reverse-engineered it from the code to become the team's subject-matter expert.
+ Prototyped a bridging API unifying five disparate databases behind a single business-entity interface (Hapi, TypeScript, Prisma), learning the full stack from scratch to build it.
+ Evaluated Go for the next-generation platform and recommended against adoption despite its technical fit, citing the org-wide rollover cost for an all-Java team.
+ Worked alongside the company's most tenured engineers on next-generation architecture and OpenAPI design after an incoming director routed proof-of-concept work my way.

### Software Engineer - Atos / Syntel (client: FedEx)
Sep 2014 - May 2020

+ Owned and operated a Tier 1 XML document platform (~60TB) across two data centers, holding flight records and the auth data other systems depended on; carried 24/7/365 on-call alone for four years.
+ Resolved most off-hours incidents by tracing faults to their real source, often proving the problem lived in a client system rather than ours.
+ Built the runtime-configurable data layer behind an internal InfoSec risk-scoring system, a field model returning confidence scores on signals like IP, location, and domain.

### Code Connector - Volunteer
Apr 2019 - Present

+ Co-designed and run The Coding Dojo, a guided mob-programming meetup for newer developers; maintain the shared solutions repo and led a Hacktoberfest push. Several participants credit the Dojo with the confidence that landed their first developer jobs.
+ Mentor developers at all levels on coding, career strategy, and advancement.

## Skills
### Languages
Java, Spring Boot, JavaScript (Vue, Nuxt, Node), TypeScript, Python, SQL, Bash, Groovy

### Cloud & Infrastructure
AWS (Lambda, SQS, Aurora/RDS, Elastic Beanstalk, API Gateway, EC2, CloudWatch), Docker, Jenkins

### Databases
Aurora MySQL, Oracle, SQL Server, Rocket UniVerse (Pick)

### Practices
Event-driven architecture (SQS/Lambda, JMS), REST, CI/CD, code-review ownership, AI-assisted development (Claude, JetBrains AI Assistant)

## Education
### University of Memphis
#### B.S. in Computer Engineering - 2013

Hands-on study of software and hardware system design, from circuits and assembly up through the presentation layer, with math coursework in probability, statistics, calculus, and differential equations.
