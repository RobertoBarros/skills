---
name: tool-pick
description: Research and compare libraries, frameworks, gems, packages, CLIs, and other software tools for a specific task. Use when asked for recommendations, alternatives, or the best tool to implement a capability, especially when the choice should favor active, popular, and well-maintained open-source projects.
---

# Tool Pick

Find trustworthy open-source options for a technical need. Start with curated "awesome" lists on GitHub, then validate every candidate in its upstream repository. Deliver a short, useful, verifiable selection—not a generic list of names.

## Workflow

1. Clarify only constraints that materially change the recommendation: language or ecosystem, license, environment, compatibility, budget, or functional requirements. If they are clear, research without interrupting the user.
2. Search GitHub first for "awesome" lists specific to the requested ecosystem and capability. Examples: `awesome Ruby PDF`, `awesome Python PDF`, `awesome Kubernetes logging`.
3. Prefer relevant, curated lists with many stars and recent maintenance. Open the list and locate the sections or entries related to the requested capability; never treat the list itself as a tool candidate.
4. Open each candidate's original repository. Do not use a fork, aggregator, or package page as the primary link when an upstream repository exists.
5. Verify that every candidate meets the requested function and is open source. Check its license, documentation, date of its latest release or commit, stars, contributors or organization, and evidence of real-world use, such as integrations, dependents, documented adoption, or an active community.
6. Compare candidates by technical fit before popularity metrics. Then favor, in order: open-source status, recent maintenance and activity, adoption and community, maturity and documentation quality, and popularity. Never call an option “the best” based on stars alone.
7. Include 3 to 6 options that genuinely meet the request. If fewer than three defensible options exist, explain that limitation instead of adding weak options.

## Research and evidence

- Use up-to-date web and GitHub research; metrics and maintenance status change over time.
- Give more weight to recent, sustained activity than to a single recent update.
- Distinguish an active project from a stable one: a mature library with few changes can still be suitable if its releases, issues, and compatibility indicate healthy maintenance.
- Identify material risks: archived projects, low activity, incompatible licenses or versions, dependency on a proprietary service, or a scope mismatch.
- When exact numbers are not readily verifiable, describe evidence qualitatively rather than inventing precision.
- When no relevant "awesome" list exists or it does not yield useful candidates, say so and continue with direct GitHub research and primary sources.

## Response format

Respond in the user's language unless they request otherwise. Start with a short primary recommendation and its main caveats. Then present 3 to 6 options in order of fit:

| Option | Why it fits | Health signals | Caveats |
| --- | --- | --- | --- |
| [Name](https://github.com/owner/repo) | Relevant capability, integration, and differentiators | Verified license, activity, community, adoption, or stars | Practical limitations |

Always include a direct link to each tool's original repository. Also cite the "awesome" list when it contributed to discovery. Finish with a clear selection recommendation, conditional on the user's constraints when appropriate.

## Example

For “which Ruby gem should I use to create PDFs?”, first search lists such as `awesome-ruby`, locate PDF tools, open their upstream repositories, and compare HTML-based generation, layout APIs, licenses, activity, and compatibility with the project's Ruby or Rails version.
