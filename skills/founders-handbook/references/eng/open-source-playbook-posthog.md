---
title: "The Open Source Content Marketing Playbook: Lessons from Posthog"
weight: 1
description: ""
Category: Open Source
Icon: ""
draft: false
authors:
  - Mark Percival
---

*Source: [The Open Source Content Marketing Playbook](https://1984.vc/docs/founders-handbook/eng/open-source-playbook-posthog)*


Discovery is the primary challenge for early to mid-stage open source startups. Engineers often believe in the "if you build it, they will come" approach to marketing their tools. The reality is different: even exceptional open source software needs marketing for users to find it.

PostHog, one of our best-performing open source portfolio companies, has mastered effective marketing content. I spent time talking with their head of content, Andy Vandervell, to better understand what makes their approach successful. There's nothing fancy or resource-intensive here - just practical strategies any technical founder can implement immediately.

### Start Here: The "Alternatives to X" List


Your first piece of content should be "The X best open source [your product space] tools" article. PostHog's most successful post ever is ["The 12 best open source analytics tools."](https://posthog.com/blog/best-open-source-analytics-tools) This format works because:

- People actively search for alternatives
- It positions you in the market
- It ranks well in search
- It's what developers actually read
Don't overthink it. List the main players, be honest about their strengths and weaknesses, and explain where your tool fits.

 **Examples:** 

- [The 12 best open source analytics tools](https://posthog.com/blog/best-open-source-analytics-tools)
- [The 9 best open source feature flag tools](https://posthog.com/blog/best-open-source-feature-flag-tools)
- [PostHog alternatives](https://posthog.com/blog/posthog-alternatives)
### The Conversion Article: "Setup for X" Articles


Forget long tutorials. Write short, targeted pieces showing how to set up your tool with specific technologies. Here's the formula:

- Pick one technology (React, Nuxt, whatever)
- Show the exact steps to integrate your tool
- Keep it under 1,000 words
- Include the actual code
- Link to related setups at the bottom
Example structure:

```markdown
Title: Using [Your Tool] with React
1. Prerequisites
2. Installation (with code)
3. Basic setup (with code)
4. Quick test to show it works
5. Links to related setups

```


This format is repeatable and scalable. Each article targets developers using specific tech stacks. More importantly, it shows them exactly how to solve their problem.

When creating technical content, there's a common pitfall: we often write with an experienced developer in mind—someone who deeply understands both our product and the technology stack they're using. This assumption doesn't match reality.

Many developers who will use your product:

- Are just getting started with the framework or technology they're using
- May be junior developers or those switching from different tech stacks
- Have limited understanding of your product's domain (analytics, testing, monitoring, etc.)
- Are looking for quick solutions rather than deep technical discussions
"Setup for X" articles and straightforward integration guides are effective because they meet developers where they are. They provide clear, actionable steps without assuming extensive background knowledge. Your content should act as a bridge, helping developers successfully implement your solution regardless of their experience level.

 **Examples:** 

- [How to set up analytics in Nuxt](https://posthog.com/tutorials/nuxt-analytics)
- [How to set up analytics in React Native](https://posthog.com/tutorials/react-native-analytics)
### Comparison Content: Tables Are King


People love comparison tables. They'll skim your article and zero in on the table. That's fine—embrace it.

Make your tables:

- Honest about pros and cons
- Clear about pricing
- Specific about features
- Easy to scan
Don't try to "win" every comparison. Be transparent about your strengths and limitations. Highlight where you excel while acknowledging areas where competitors might have an edge. Developers value authenticity and can easily detect marketing spin or FUD. A balanced, truthful comparison builds credibility and trust with technical audiences, ultimately leading to more conversions than overly promotional content.

 **Examples:** 

- [PostHog vs Hotjar](https://posthog.com/blog/posthog-vs-hotjar)
- [PostHog vs Amplitude](https://posthog.com/blog/posthog-vs-amplitude)
- [PostHog vs Matomo](https://posthog.com/blog/posthog-vs-matomo)
### What Else Works


A few other things we've learned from PostHog:

1.  **Write about problems you solve** , even if only a small audience searches for it. A high-intent reader beats high traffic every time.
1.  **Be authentic and transparent** —PostHog includes a "Changelog" at the top of their comparison articles
1.  **Track what matters:** 
    - Where do people go after reading?
    - Do they hit the docs?
    - Do they sign up?

1.  **Don't worry about posting cadence.**  Good content beats regular content.
1.  **For social sharing:** 
    - Use personal accounts, not company ones
    - LinkedIn works better than Twitter
    - Newsletter promotion often beats social

### The Reality Check


SEO takes time. Don't expect immediate payback from these articles. In the early days, focus on sharing what you learn and helping solve specific problems. The search traffic will come later.

Your content strategy isn't about being clever or original. It's about being useful to developers who need your tool. Focus on that. The occasional thought piece that shows up on Hacker News might be good for hiring and investor relations, but your end user isn't on Hacker News all day. They're just trying to solve a problem, so focus on getting your solution in front of them.
