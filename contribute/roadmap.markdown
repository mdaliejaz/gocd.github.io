---
layout: default
title: Roadmap
date:   2014-01-07
title_tag: Roadmap | Configuration Management Repository | Go CD
meta_tag_description: Go Continuous Delivery roadmap with proposed timeline and resources provides platform that helps us release software to production on demand
meta_tag_keywords: continuous delivery roadmap, continuous delivery roadmap, configuration management repository, go
---

```
Last Updated: 3-Feb-2015
```

The following are proposed features for Go. While this doesn't mean we will not pick up things that are not in the list, this is what we would like to focus most of our energy on.

### Feature Set

#### Agent Management
In a CI/CD setup agent management is the hardest part. Remembering what is installed on what agent, knowing when an agent goes down, accessing agent machine to do some changes are a few things that would like to give first class support for.

* Notification of status when a new agent is available (pending) or goes missing - the [notification end-point](http://www.go.cd/documentation/developer/writing_go_plugins/notification/notification_plugin_overview.html) is available. Need to add "agent status change" notification to it.
* Capabilities / Resource (add, edit, remove) - detect software available on agent along with versions & auto update resources of agent
* Key management - manage ssh keys
* Console - to make changes on agent without having to ssh to the agent

#### Better support for Tests
The biggest time consumer in any CI/CD setup is running tests. It has become fundamental practice to write tests and every new framework supports writing & running tests first. Which means there are more tests to run & make sense of the results. We want to provide features to ease the pain.

* Parallelization - out of box support for TLB? custom runner for each type (junit, rspec etc.) which contacts Go server asking for next test to run? - Go supports '[run X instance](http://www.go.cd/2014/10/09/Distrubuted-Test-Execution.html)' of a job which could be used to distribute tests using TLB. Need to add first class support for test distribution.
* Intelligent test runs - Run tests in failed first order, Re-run failed tests etc.
* Real time reports - how many ran, how many failed & which ones failed - while the job is running
* Parse test reports - provide pluggability for all kinds of test reports/migrators for other test report formats. Currently only XUnit format is supported. - Something on the lines of [xunit-converter](https://github.com/srinivasupadhya/xunit-converter-task)?
* Test metrics - possibly list flaky tests, show time consuming tests etc.

#### Plugins
Go supports 'Package Repository' & 'Task' extension points. These are the next:

* Notificaiton extension point [#867](https://github.com/gocd/gocd/issues/867) - done. going in 15.1.0.
* Delete artifact extension point [#410](https://github.com/gocd/gocd/issues/410) - ongoing
* SCM extension point [#818](https://github.com/gocd/gocd/issues/818) - ongoing

#### APIs
The design of APIs would be such that the same could be used by any 3rd party to interact with Go Server. This would basically mean Go Server can run in head less mode allowing developers to write their own UI. The order in which we would like to go about doing this:

* API for pipeline creation - CRUD for group, pipeline / template, stage, job, task (along with env. var & parameters), material config
* API for agents - add resource, environments [#264](https://github.com/gocd/gocd/issues/264)
* API for environment dashboard
* API for search of pipeline based on parameters (checkin - SHA, message, author / pipeline - counter, label)
* API for compare pipeline

### Features

#### Dashboard Revamp/Rewrite
People spend most of their time on Go on dashboard page. With the number of pipelines & users increasing, the dashboard page needs to be optimized for performance, while giving as much info as possible in the best possible way for its consumption.

* Rewrite dashboard to hit API instead of getting the whole markup.
* Move some logic to client side to reduce load on server. more intelligent updates rather than full update?
* UX improvements

#### API first design
We want to make the Go Server UI interact with the backend through APIs, even more than it does now. This should provide some performance benefits & better user experience.

### Performance

#### Agent improvements
Improve Agent Server communication to reduce the problem of too many agents pinging the server at same time during start up & too many requests (1 ping + 1 work request = 2 requests / sec / agent) from agents.

* Thundering herd - implement exponential backoff while registering so that Server is not swamped with requests.
* Websocket - move from polling to server push model

#### CCTray performance improvements [#795](https://github.com/gocd/gocd/issues/795)

#### Go Config read-write performance improvements [#838](https://github.com/gocd/gocd/issues/838)

### Tech Debt

#### Jetty upgrade [#400](https://github.com/gocd/gocd/issues/400) - ongoing

#### Migrate from iBatis to Hibernate [#401](https://github.com/gocd/gocd/issues/401)

#### Migrate UI from velocity to rails [#434](https://github.com/gocd/gocd/issues/434)
