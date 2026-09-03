---
layout: home
title: Home
nav_order: 1
last_modified_date: 2022-09-18 20:35
---
Welcome to the TReNDS cluster documentation. It provides example job
submission scripts and guide to running various applications
interactively on the GSU/TReNDS cluster. This is heavily influenced by
the [Georgia Tech PACE cluster
documentation](https://docs.pace.gatech.edu/).

**Before getting started, please check the [cluster usage policies](https://trendscenter.github.io/wiki/docs/Cluster_do's_&_don'ts.html)**
For a recording of a workshop covering the steps in this wiki, as well as usage policies, please check [here](https://gsumeetings.webex.com/gsumeetings/ldr.php?RCID=4e8134fa43d416208d6c3712c57d1e5c) (GSU credentials required).

**Having issues?** First, check out our [FAQ](docs/FAQ.md). If you can't find your solution there, try searching the wiki next. If you can't find a solution to your
problem in the wiki, then check the #hpc-tips channel in the TReNDs slack. 

{: .tip }
Please look for the "last modified" date at the bottom of any page to be sure that the information is updated.

![clusterFlow]({{ site.baseurl }}/assets/images/clusterFlow.jpg)

## New to the cluster?

Before you start, please take a look at this documentation and this page in particular: [Getting Started](docs/Getting_Started)

It may look overwhelming but in fact, the rules are simple:
- Run your jobs ONLY through SLURM
- Experiment and develop on development nodes (we have 2 CPU nodes designated for that and one GPU node)
- NEVER EVER run any computation on the login node 🙂

The other details are in the documentation. Also, you may want to join our cluster slack channel [#hpc-tips](http://trendscenter.slack.com/#hpc-tips) to ask questions if in trouble.

## Contributing

You can now easily contribute to this documentation! Just fork the repo [https://github.com/trendscenter/wiki.git](https://github.com/trendscenter/wiki.git) and make pull requests. If you notice any error or wrong information on any page, please let us know by creating an issue in the same repo.



