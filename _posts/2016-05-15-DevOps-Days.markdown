---
layout: post
title:  DevOps Days
date:   2016-05-21
tags:
  - conference
  - devops
---

### DevOps Days Seattle 2016

I recently went to DevOps Days Seattle. And I went in cold. That is, my understanding of DevOps – the philosophy and the technology – was (and remains, though it has improved) limited.

<br>
For example: before this conference I thought about DevOps only in terms of the tooling – both the new technologies publically available and the tools being developed by our very own DevOps unicorns Dale and Wei. These powerful technologies were definitely exciting to me, but without the context of work on other Dev or Ops teams I could not fully appreciate the issues they address. In short, I hadn’t given an appropriate amount of thought to why these technologies were so hot, so revolutionary – this was very un-DevOps of me.

<br>
Below is a summary of each of the main presentations, followed by speaker suggested reading.


### Nicole Forsgren (Chef) - Measuring All The Things
Nicole Forsgren began the conference with a talk on metrics. Her work is based upon the belief that “you can’t improve what you don’t measure”. So, in her first year at Chef, she took a baseline measurement in three major categories: external (measured by commercial adoption), internal (measured by shiping), and cultural (measured by the Westrum survey). She explained that metrics should be curated to reflect the company’s current goals and values and that they should be reevaluated often to prevent stagnation. Forsgren seemed to look at metrics not only as a way to improve but as a way to avoid failure. For, in her experience, “once culture falls apart, technology falls apart - about six months out.” Her most important point was that metrics date quickly, but their usefulness is unparalleled when you are measuring the right thing.

### Joanne Molesky (ThoughtWorks) - An Unlikely Couple: DevOps & IT Audit?
Joanne Molesky gave a great talk on auditing DevOps teams’ products. Good auditing, she started, has one simple goal: to reduce risk. So the first (and most important) step in auditing a DevOps product is to acknowledge that technology is no longer a bottleneck and therefore the existing security infrastructure in place to reduce risk is outdated. This infrastructure, Molesky says, is risk averse by nature and does not have the capacity to make informed decisions about devops products, so they simply say no. Her advice is to create a common understanding, to learn the language of audit (because a developer learning the language of an auditor is far more likely than the inverse), and to focus on the intent of what each control is trying to achieve.

### Pauly Comtois (Hearst) - Building an Enterprise DevOps Community
Pauly Comtois discussed bringing DevOps to your entire organization. His talk emphasized leaving no group out: from executives to managers to developers. In order to become the “lean, agile, machine” you want to be he says the more important steps are aligning goals and flattening responsibility. And they key to this, he says, is culture: “High performing organizations get their culture DevOps culture right first. They hire for cultural fit first, then grow skills rather than vice-versa.”

### Ben Rockwood (Chef) - The Power of A3
Ben Rockwood talk was rooted in the belief that the key to doing anything well is intentionality and therefore systems and improvements that are not designed are usually bad or broken systems. At the heart of his talk were the Japanese concepts of Kaizen and Kaiaku. Both are forms of progressive change which aim to improve the work environment and work product.

- Kaizen are small and continuous changes made to improve the system. Practicing Kaizen is a way of life and should be embedded in company culture.
- Kaiaku is a major change: a drastic measure taken when making small changes to the existing system would not help.

But how to asses what and when to change? Rockwood recommends the A3: a problem solving device that helps clarify and record the problem. Rockwood emphasized that the benefit of this is not the form, but guidance through a thinking process of current state, future state, gap analysis, and solutions implementations. And the artifact itself then acts as a touchstone that constrains your work/focus throughout the process.

### Courtney Kissler & Matt Hornby (Nordstroms) -Living In A Hybrid World
Courtney Kissler and Matt Hornby from Nordstroms discussed how breaking small pieces off the Nordstroms' monolith has improved their overall time to ship. Realizing that they could not modernize everything at once the Nordstroms' team started with small changes: removing unnecessary overhead and obstacles. By embracing Conway’s Law: “organizations which design systems ... are constrained to produce designs which are copies of the communication structures of these organizations”, they determined two aspects to be critical to their success. The first was creating a cross-discipline team, making sure that access to pertinent knowledge was unfettered. The second was flatten decision making by involving implementation teams in problem solving.

### Jason Hand (Victorops) - Understanding Cognitive Bias Found In Judgement & Choice
Jason Hand spoke about the mindset needed to address pages under pressure. In these situations our minds are likely to rationalize rather than act rationally, relying on mental shortcuts and heuristics. In order to avoid the pitfalls of cognitive bias (which he illustrated in very entertaining ways) he advocated that teams conduct postmortems (focused on how not why), create runbooks, and participate in game days regularly. For a taste of Jason’s points on cognitive bias watch this then this.

### Brendan Burns (Google) - How Container Clusters, Like Kubernetes Change Operations
Brendan Burns gave an overview of Kubernetes. It was a version of the presentation he gave at
CoreOS Fest 2015 He talked about Kubernetes as part of the solution to the unintended consequences of breaking apart dev and ops and then coupling them back together. There was also a fun demonstration with a Kubernetes and a stack of Raspberry Pis. If you’re interested I found a tutorial here.

### Michael Kauffman (Big Nimble) - Past The Hype: A Better Way To Think About Big Data
Michael Kaufman defined big data in terms of five types: language, media, sensor, geographic, and pattern matching. These types of data, used either individually or in conjunction with each other, are very powerful tools. He suggested that the key to leveraging these forms of data is to break free from functional rigidity. By using data in new and unintended ways to you can unlock a hosts of new insights. For example: one commercial realty company reduced the number of tenants defaulting on leases by using sensor data from elevators. By detecting when companies were laying off employees (less passengers disembarking the corresponding floor) they were able to approach those companies with an offer to decrease their rental space. This ultimately led to preserving the company’s client base and revenue.

### Speaker Suggested Reading:
- Data Driven – Mason, Patil
- Lean Enterprise – Molseky, Humble, O’Reilly
- Mind and the World Order: Outline of a Theory of Knowledge-  Lewis
- Thinking Fast and Slow - Kahneman
- Understanding A3 Thinking – Sobek, Smally
- Managing to Learn - Shook
- Site Reliability Engineering – Beyer, Jones, Murphy, Petoff
