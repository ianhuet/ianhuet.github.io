---
title: "To PR or not to PR"
date: "2023-05-26"
excerpt: "Is that the most meaningful question?"
---

# To PR or not to PR
Is that the most meaningful question?

#### TL;DR
> Debate on the Pull Request (PR[^1]) process is endless. Despite all the arguments against it I'm for PRs. Reflecting on this position brought me to the [Ship / Show / Ask](https://martinfowler.com/articles/ship-show-ask.html) adaptation of the process. It offers an easily communicated middle-ground between traditional PRs & mainline CI. Yet, coming to this middle-ground highlighted how most branching strategy debate is more about human practice than technical guard rails.

---

For many years PRs have been the only process I've worked with for team development work. A recent internal project initially followed that same trend. This served us well in terms of sharing knowledge as the project rapidly evolved without introducing delays. However, the development of the projects core functionality fell to an engineer who drove a merge to mainline approach instead.

I found this challenging for a variety of reasons. Not least because it flew in the face of what I had become so accustomed to being the 'right' way. I urgently looked for a counter argument. During that process I found several things:

- My initial response was dogmatic.
- For every arguement [against PRs](https://blog.arkency.com/disadvantages-of-pull-requests/), there is an equally valid counter arguement [for PRs](https://productive.io/engineering/blog/pull-requests-the-good-the-bad-and-really-not-that-ugly/).
- Looking again at possible [branching strategies](https://martinfowler.com/articles/branching-patterns.html) led me to [Rouan Wilsenach's Ship/Shop/Ask](https://martinfowler.com/articles/ship-show-ask.html)

As a declared PR advocate this offers a more nuanced approach than I'd previously held. It requires no new technology to implement, repository merge configuration tweaks only ([GitHub](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges), [GitLab](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/settings.html), [BitBucket](https://support.atlassian.com/bitbucket-cloud/docs/pull-request-and-merge-settings/) for example). It's easy to communicate. It retains the routine checks & balances of PRs, personally I'd only ever see the 'ship' option being used for small hotfixes. It offers more latitute, and more rapid throughput, among experienced and trusted engineers.

Yet, regardless of the branching strategy [well honed collaboration practice is fundamental](https://dockyard.com/blog/2020/10/20/creating-effective-pull-requests) to successful progress. In my opinion the most important aspects of that practice include small merge diffs, automated code linting, professional reviews (prompt, respectful, thorough, and practical), and monitoring via source control metrics. Further to this, varied forms of communication (advance planning, retrospective session, product focused, technically oriented, formal, informal, etc.) are good for team health. Ideally encouraged or scheduled if needs be, without straining delivery commitments of course.

## Take aways

- Only firmly hold a position when no other options are available, and that position can be holistically supported.
- Effective teams align on a balance between throughput, output quality & DevEx.
- The 'right' process is specific to each team or organisation, and best served by being open to evolution.

### References:

- [Pull Request vs. Merge Request: Definition, Differences, and More](
https://www.simplilearn.com/pull-vs-merge-request-definition-differences-benefits-article#what_is_a_merge_request)

- [Disadvantages of Pull Requests](https://blog.arkency.com/disadvantages-of-pull-requests/)

- [Pull Requests — The Good, the Bad and Really, Not That Ugly](https://productive.io/engineering/blog/pull-requests-the-good-the-bad-and-really-not-that-ugly/)

- [Why code reviews matter (and actually save time!)](https://www.atlassian.com/agile/software-development/code-reviews)

- [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)

- [Ship-Show-Ask](https://martinfowler.com/articles/ship-show-ask.html)

---

[^1]: Pull Request (PR): A notification given by developers when they are done building a feature. 
