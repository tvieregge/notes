Should we give everyone at Voltus access to our GitHub organization? #8369
engineering monorepo wiki accessibility #7639
FAQS #7854
Updating voltus/pkg README #8446

### Problems to address with docs
- keeping them up to date 
- Getting new engineers up to speed
- Getting engineers that switch teams/domains up to speed
- Setting standards
- Knowledge repository
- documentation fragmentation (old docs, differnet places, new places)
- we need documentation that shows how to recreate a workflow
- we need documentation for all APIs
- we need documentation that provides an overview of system architectures
- we need documentation that is searchable
- we need documentation that shows service dependencies
- we need documentation that shows how to do a specific thing (e.g. how to add DD tracing to your application)
- organic growth? How do we give it positive feedback

Thoughts, from [[tim boring]]
> Similarly, thinking about our current docs, do they meet our goals? Are they up-to-date? Are they easy to find/discover? (Are they kept on Max's NixOS machine?) If these goals are not met, why not? What obstacles are keeping us from meeting these goals? As Meri asked, is it a matter of motivation?
> Might make sense to take both approaches simultaneously. Maybe short term we can agree on a set of docs that every service should have. For example, in the Gridpoint Site Updater service, I created a docs directory in the project repo and put three docs

### goals
- Documentation should be kept up-to-date
- Documentation should be easy to find/discover

### what we use
- sphinx  [registry](https://github.com/voltusdev/voltus/blob/master/wiki/dev/sphinx-docs.md)
- readme
- wiki

### Platforms to look into
- https://docs.readthedocs.io/en/stable/index.html
    - https://docs.djangoproject.com/en/3.2/
-  gitbook: [github integration](https://docs.gitbook.com/integrations/github)

### Documentation Success
1. It exists
2. Is up to date
3. Is usable

I think documentation needs to be those things, in that order. This has some implications like low friction to update docs > seachability. 

There a limits to this ordering, but an example clarifies:

> A flat text file with al the information you could want that's always up to date would be pretty useful. 

This has very high #1 and #2, but the lowest (reasonable) #3

## Golden Path documentation
- created a tutorial on the recommended way of using our services
- opinionated and supported’ path to ‘build something’ (for example, build a backend service, put up a website, create a data pipeline)
- the primary job of the Golden Path tutorials is to walk [[onboarding for fast growth]] engineers through the Golden Path 
- Ownership is hard to coordinate
- could lead to "golden state": a set of checks to see if the system is on the "golden path". Like a linter, but ingrained with the knowledge of the company + tech stack?
- could also lead to higher level docs: end to end golden path for a new product. This would be targeted at a team, rather than the normal golden path doc being targeted at an individual
- This tool uses the wizard format to reduce the number of decisions engineers have to make to build backend services, application features, data pipelines, machine learning projects, and web apps

### Success Factors
**Clearly defined audience**: write for a new eng, still works for other people
**Singular (main) purpose**: “The Golden Path is the opinionated and supported path to build your system and the Golden Path tutorial walks you through this path.”
**Step by step**: Show *every* step. If its too long then the process is the problem
**One per dicipline**: they could imagine other ways like: one per eng job; one on testing, one on coding etc.
**It's about education**: explain (link to?) what going on under the hood if there's complicated "magic"
**special status**: it's the most import doc
**feedback and testing**: every new eng goes through it


### Spotify uses
- TechDocs
- Backstage

### Measuring: How good are our docs, what are the problems
- we could ask people
- make a survey
- have a running log (slack channel?) that people put their doc failures on
- put something on the doc pages (too fragmented for this to work)
- how long until first: merged pr, new service

### Things that golden path docs wouldn't do
- specs

### Things that it would do
- be up to date 
- Getting new engineers up to speed
- Getting engineers that switch teams/domains up to speed
- Setting standards
- documentation fragmentation (old docs, differnet places, new places)
- we need documentation that shows how to recreate a workflow
- we need documentation that shows how to do a specific thing (e.g. how to add DD tracing to your application)


Thanks to: liza, bill, meri

CI tests for docs?
https://voltus-team.slack.com/archives/C279HBG7R/p1623165448239300

Put golden path instructions into docker image and test them?
    literate code?
no point to checked in wiki, readmes cover the use case of checked in docs

Most of what I seek in documentation is three things:
1 - How to recreate a workflow, and what points of friction there might be and how to overcome them
2 - API reference
3 - What the hell is this thing please give me a general overview/architecture

> documentation issues are often better solved with process improvements (i.e. clear expectations around what should live where) and I haven't seen them get solved with different tools

from [[sheridan]]

### Exmples
- https://voltus-team.slack.com/archives/C279HBG7R/p1623165448239300