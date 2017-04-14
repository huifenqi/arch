# 13. The sense of Done

Date: 14/04/2017

## Status

Proposed

## Context

We face this situation very often?

1. I’m already fixed this, it’s in testing;
2. I’m already add this monitoring plugin in the repo, it’s deployed on staging, let’s watch for a few days, then deploy on production;
3. I’m already move this service to new machine, I will clean the old machine later.

Sounds familiar? Yes, very often.

Is that all done? No, it doesn’t.

## Decision

1. talk this all the time, let team member have this sense;
2. make specifications for each domain.

## Consequences

Create specifications from our experience.

An Done-Done example with `User Story`:

1. stories and AC reviewed (DEV);
2. All AC implemented (DEV);
3. Code reviewed (Dev);
4. Tests passed (Dev+QA+CI);
5. No bugs left (QA);
6. Deployed to production (Dev);
7. Accepted (PM).

Refs:

* What is Done Done? [http://chrislema.com/what-is-done-done/][1]
* Agile Principle 7: Done Means DONE! [http://www.allaboutagile.com/agile-principle-7-done-means-done/][2]
* The Definition of READY [http://blog.xebia.com/the-definition-of-ready/][3]
* What is the Definition of Done (DoD) in Agile? [http://www.solutionsiq.com/what-is-the-definition-of-done-dod-in-agile/][4]
* Scrum Crash Course [https://www.slideshare.net/beITconference/infragistics-scrum-crashcoursebeit2014][5]

[1]:	http://chrislema.com/what-is-done-done/
[2]:	http://www.allaboutagile.com/agile-principle-7-done-means-done/
[3]:	http://blog.xebia.com/the-definition-of-ready/
[4]:	http://www.solutionsiq.com/what-is-the-definition-of-done-dod-in-agile/
[5]:	https://www.slideshare.net/beITconference/infragistics-scrum-crashcoursebeit2014