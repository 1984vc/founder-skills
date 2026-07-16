---
title: Engineering Best Practices at Seed Stage
weight: 1
description: ""
Category: Engineering
Icon: document-text
draft: false
authors:
  - Mark Percival
---

*Source: [Engineering Best Practices at Seed Stage](https://1984.vc/docs/founders-handbook/eng/best-practices-seed)*


Many seed-stage founders believe engineering excellence is a luxury they can't afford. They're wrong. The technical debt you accumulate in your first 18 months will determine whether you can scale or whether you'll spend your post Series A rewriting everything from scratch (if you even got there). Below we'll lay out the non-negotiable engineering practices that separate companies that scale from those that stall, based on patterns we've observed across our portfolio.

## 1. Testing is not optional - It's a competitive advantage


I routinely meet founders who view testing as something to "add later." This is backwards.  **Testing is what allows you to move faster, not slower** . Without tests, every deploy becomes a prayer, every refactor becomes an archaeological dig, and your best engineers spend their time firefighting instead of building.

Here's the counterintuitive truth: the right time to implement testing is when you have 2 engineers, not 20. Why? Because retrofitting tests onto an untested codebase is like trying to add a foundation to a house that's already built. It's painful, expensive, and never quite works right.

### Start with Critical Path Coverage


You don't need 100% test coverage on day one. Focus on the code that would take your company down if it broke:

- Payment processing flows
- User authentication and authorization
- Core business logic that drives revenue
- Data integrity checks (This is a big one, it's very hard to fix data later)
> 🚨 Backfilling tests? Junior engineers shouldn't be writing these tests, you or your most senior engineers should. Engineering leadership always starts from the top! 


 **Practical rule:**  Every new feature ships with tests. No exceptions. For existing code, add tests when you touch it. We don't need >90% today, but it's critical that we make forward progress on it each week.

## 2. Code Reviews: Your Secret Weapon for Team Velocity


Many seed-stage companies treat code reviews as a formality - a box to check before merging. This misses the point entirely.  **Code reviews are how you scale engineering knowledge across your team** .

The biggest mistake I see: making your CTO or lead engineer the bottleneck for every review. This doesn't scale past 3 engineers. Instead, implement peer review from day one. Yes, your junior engineers will miss things initially. That's fine. They'll learn faster by reviewing code than from any mentorship program.

### The Review Process That Actually Works


- Every PR gets reviewed within 4 hours during business hours
- Reviews focus on business logic, not formatting (but you should already be linting)
- Junior engineers review senior code too, it's how they learn the expectations.
- Comments don't have to be critiques, they can ask questions or share learnings - e.g. "The API team is also using this endpoint"
- PRs are not formally reviewed until they are ready. Asking for feedback is fine, but when you're ready for the review it needs to be ready to merge.
> 💡 LGTM and "👍" are not reviews, find something to add to the conversation!


## 3. Engineering Discipline: The Basics That Compound


The difference between a seed-stage company that scales and one that doesn't often comes down to boring fundamentals. These practices seem trivial individually but compound into massive advantages:

### Non-Negotiable Practices


 **Semantic Commits:**  Your git history should tell a story.  `fix bug`  is not a commit message.  `Fix: Payment webhook retry logic for failed Stripe events`  is. Six months from now, when you're debugging a production issue at 2 AM, you'll thank yourself.

 **Concise PRs with a single focus:**  One PR, one purpose. I've seen too many "quick fixes" bundled with feature work that introduce bugs because reviewers couldn't properly evaluate 1,500 lines of mixed changes.

 **Automated Checks:**  Your CI/CD pipeline should run:

- Linting (catches style issues)
- Type checking (if applicable)
- Tests (obviously)
If any check fails, the PR doesn't merge. No exceptions, not even for the CEO.

 **Changelog:**  You can automate most of this with semantic commits. Everyone in the company, not just the engineers should be able to review progress and understand what's happening to the codebase.

### Setting the Standard


Founders need to set expectations early:  **engineers will only perform at the level you expect** . If you accept sloppy PRs, broken builds and no testing, that becomes your culture. Once established, engineering culture is nearly impossible to change without replacing people.

The best approach? Have your strongest engineer model these practices religiously for the first 3 months. Others will follow. If you don't have someone who can set this standard, your first hire should be someone who can. In 3 months, anyone that can't meet these standards should be let go.

## 4. AI Is Your Force Multiplier


It's 2025. If your engineers aren't using AI tools, you're leaving productivity on the table. I'm surprised by seed-stage AI companies that themselves aren't using AI to its fullest. It's not just AI coding, it's automating documentation, support work and building workflows that maximize productivity.

### The AI Setup That Actually Delivers


Every engineer should have:

-  **AI coding assistant**  (Cline, Cursor or Claude) with project-specific rules
-  **Rules file**  that gets updated weekly with architecture decisions, coding patterns, and company conventions
-  **Documentation generation**  for all public APIs and complex functions
-  **Test generation**  for routine test cases. AI is great at coming up with edge cases. AI-generated code tends to be verbose, which is perfect for tests.
> 💡  **AI doesn't replace engineers, it replaces engineering tedium** . Your engineers should be solving business problems, not writing boilerplate.


## 5. Technical Leaders, not Managers


If your current team can't implement these practices, you need different people. This sounds harsh, but it's kinder than the alternative: burning 18 months and $2M building a product that needs to be rewritten from the ground up.

The ideal candidate should be:

- A true believer in engineering best practices. This isn't just a process change, it's a cultural shift. People can recognize when someone isn't genuinely committed.
- Can teach and mentor, not just code. Avoid anyone that wants to just heads-down task or solve complex architecture problems, communication is critical.
This person doesn't need to be a CTO. A strong senior engineer or engineering manager can reset expectations and establish the right culture. But someone needs to own this transformation.

## Common Objections (And Why They're Wrong)


 **"We don't have time for this."**  You don't have time  *not*  to do this. Every month you delay makes the eventual fix many times harder.

 **"Our customers don't care about our engineering practices."**  They care about bugs, downtime, and feature velocity. Good engineering practices directly impact all three.

 **"We'll fix it after we find product-market fit."**  Companies that find PMF with bad engineering practices often can't capitalize on it because they can't scale fast enough.

## The Other Direction


There's an equally dangerous trap that often ensnares well-intentioned leaders from larger organizations: process theater. Instead of cultivating engineering excellence through culture, they impose rigid metrics and mandatory tooling. Tests aren't written because engineers understand their value - they're written to hit arbitrary coverage targets.

This checkbox mentality is poison for early-stage companies. When engineers write tests solely to satisfy coverage reports, you haven't built a culture of excellence, you've built a culture of compliance. Your team stops asking "How can we build the best product?" and starts asking "How can I get this pipeline to pass?"

The irony is that these leaders often implement the  *artifacts*  of good engineering (test coverage metrics, code review templates, velocity tracking) without understanding the  *principles*  that make them valuable. Real engineering excellence comes from engineers who write tests because they've been burned by bugs, who review code carefully because they care about their teammates' success, who document clearly because they remember their own confusion.

At seed stage, every process you add should make engineers more effective, not more compliant. If you find yourself managing metrics instead of mentoring engineers, you're building the wrong culture.

## The 30-Day Implementation Plan


It's not unusual for companies to find themselves at Series A with a small amount of tests, a brittle codebase and a burnt-out engineering team (it's why we wrote this guide). But it makes this next part much more important.

Here's our quick plan to right the ship in 30 days (or die trying):

 **Week 1:** 

- Set up basic CI/CD with linting and type checking
- Implement PR review requirements
- Write tests for your most critical flow
 **Week 2:** 

- Add semantic commit enforcement
- Set up AI coding assistants for all engineers
- All new code comes with tests
 **Week 3:** 

- Achieve 50% test coverage on critical paths
- Establish code review SLAs
- Create your first CHANGELOG (automate it)
 **Week 4:** 

- CI/CD pipeline should include AI code reviews to supplement human ones
- Conduct a retrospective on the new processes
- Adjust based on team feedback
## The Bottom Line


Engineering excellence at seed stage isn't about perfection - it's about building habits that in turn build great culture. Every thoughtful test, every thorough code review, every clear commit message compounds into something bigger: a culture of craft. While great engineering won't save a startup with no product market fit, poor engineering culture will absolutely kill one that does. The practices you establish today become the foundation your team stands on tomorrow.
