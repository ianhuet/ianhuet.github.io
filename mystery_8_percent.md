---
title: "The Mystery 8%"
date: "2023-05-16"
excerpt: "Beware the gap between code & test coverage"
---

# The Mystery 8%
Beware the gap between code & test coverage

## TL;DR
A [test coverage threshold](https://jestjs.io/docs/configuration#coveragethreshold-object) can be a useful tool to drive improved test coverage. Yet it is only part of the process, it is important to be vigilant for large increases as code coverage reports are calculated on the amount of code executed, not on the amount of code tested.

Sudden jumps in code coverage are an indicator of poor practice. Unchecked this is counter productive.

---

Amongst the many challenges in quantifying code quality [code coverage](https://istanbul.js.org/) stands out as one of the most easily calculated. As a result coverage is commonly considered an important indicator in software testing in terms of quality and effectiveness. However, there is a subtle but important difference between code coverage and test coverage that will result in misleading metrics and misplaced confidence.

Ahead of fully automated test quality tooling being installed I have been completing periodic test quality reviews. During one of these reviews I spotted an 8% jump in coverage. While there had been great progress made in expanding our test coverage this was exceptional - which raised a flag, it was just too good to true! And it begged the question, where did this bump come from?

After tracking back through the commit history the bump was isolated to a PR: a single, small PR. The next question was what was the exact source. In this instance it was an implementation detail. The exceptional code coverage bump had highlighted a high level component import that was not the best option to have used. The result being a considerable increase in the amount of code being imported but none of this code was being actively tested: code coverage versus test coverage.

Thankfully there was an easily completed alternative that delivered the same functionality without skewing test coverage. With this update applied the coverage returned to the expected level. Though at a reduced level it is a more accurate representation of the actual test coverage.

## Take aways:

If the coverage change was downward it would likely have thrown an error. Yet an 8% increase raised no alarms at all.

- [Automatically reporting test coverage on all PRs](https://github.com/marketplace/actions/jest-coverage-report#customizing-test-script) would surface this alleviating the manual review overhead.
- Always bear in mind that 'code coverage' is a measure of code executed when tests are run, not 'test coverage' which is the actual amount of code tested.
- Beware the potential for any metric to be misundersood. Especially important to remember when using an automated coverage threshold to press for more test coverage.

### References:

- Why Test Coverage is an Important part of Software Testing?
https://www.simform.com/test-coverage/

- How to Ensure Test Coverage
https://www.testim.io/blog/how-to-ensure-test-coverage/
