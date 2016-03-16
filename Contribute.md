# Contribute #

Multiple types of contributions are possible :

  * Using it in your product or project and providing feedback.
  * Code & Algorithms: Core Projects, Incubator projects, Frameworks
  * Use cases, feature requests: Roadmap influence
  * Community Support, bug fixes, forum posts: Help to be helped
  * Documentation: Everyone needs good docs, Code is a moving targed.
  * Testing (Perf, load, security, unit tests, interop, ...) / CI

Here is specific types of contributions that requires a little more details if you want to get involved

  * Fixing Bugs : See [Contribution Process below](Contribute#How_to_check_out,_change,_review,_and_commit_code.md). You can discuss your Issue first on [the mailing list of Mobicents public google group](https://mail.google.com/mail/?view=cm&fs=1&tf=1&to=mobicents-public@googlegroups.com)
  * Reporting Bugs : To report a bug, if possible, provide a small example that illustrates the bug. You can pattern the test case usually along the lines of https://sipservlets.googlecode.com/git/sip-servlets-test-suite/testsuite/src/test/java/org/mobicents/servlet/sip/testsuite/simple/ShootmeSipServletTest.java. Having a test case handy speeds up the bug fix. Your test case will be included in the project as a test case. open an Issue as defined in the section below so other users can know about the issue and its status. Please attach your test case or bug description with debug log files there.
  * Contributing Extensions and enhancements (i.e. support for Sip extension RFCs and drafts that are not covered by Mobicents SIP Servlets) or Contributing code snippets and examples or Contributing test cases to be included with the distribution: See [Contribution Process below](Contribute#How_to_check_out,_change,_review,_and_commit_code.md). Also open a thread on [the mailing list of Mobicents public google group](https://mail.google.com/mail/?view=cm&fs=1&tf=1&to=mobicents-public@googlegroups.com) to discuss it with the community and Mobicents Core Team Members.

Your contributions will be acknowledged individually in the code (as a comment) and in the [Acknowledgement page](http://www.mobicents.org/acknowledgements.html).


# Opening an Issue #

[Open An Issue Here](http://code.google.com/p/sipservlets/issues/entry)

# Becoming a Contributor #

In order to become a contributor with write access to the code, you will need to have demonstrated an understanding of the codebase and testsuite by participating in the design discussions and submitting patches for bugs/enchancements before we will grant developer access.

Contributing to Mobicents requires you to accept [the TeleStax Contributor Agreement](http://telestax.com/opensource/) (bottom of the page).

Next, Start Contributing by following the [Contribution Process below](Contribute#How_to_check_out,_change,_review,_and_commit_code.md)

# How to check out, change, review, and commit code #
## Introduction ##

Mobicents projects use Git, a distributed version control system. What this means is that, even though this page hosts a central repository, there can be many clone repositories with changes of their own, and then some of those can be merged back into the main repository.

**The great part is that you can start contributing and create our own clone without having write access to the Mobicents repository**

This document describes the workflow for checking out code, making clones, reviewing patches, and committing code.

## Checking out Mobicents SIP Servlets (Linux) ##
For non-committers, checking out code is simple.

### Install Git ###

Follow the installing Git instructions. Ubuntu users can simply type:

```
sudo apt-get install git-core
```

Configure Git to convert line endings on commit

```
git config --global core.autocrlf input
```

### Checkout the code ###

Follow the [checkout instructions](http://code.google.com/p/sipservlets/source/checkout) to check out the code  :

```
git clone https://code.google.com/p/sipservlets
```

### Committing code ###

The following License Header has to be placed on top of each source code file contributed
```
/*
 * TeleStax, Open Source Cloud Communications
 * Copyright 2011-2014, Telestax Inc and individual contributors
 * by the @authors tag.
 *
 * This program is free software: you can redistribute it and/or modify
 * under the terms of the GNU Affero General Public License as
 * published by the Free Software Foundation; either version 3 of
 * the License, or (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU Affero General Public License for more details.
 *
 * You should have received a copy of the GNU Affero General Public License
 * along with this program.  If not, see <http://www.gnu.org/licenses/>
 *
 * This file incorporates work covered by the following copyright contributed under the GNU LGPL : Copyright 2007-2011 Red Hat.
 */
```

The model we've chosen for developing Mobicents SIP Servlets is the following:

Each contributor creates a Google Code Project Hosting clone of the main Mobicents SIP Servlets repository.

This clone is hosted on Google servers, and can be created by clicking **Create a clone** button from  http://code.google.com/p/sipservlets/source/checkout or http://code.google.com/p/sipservlets/source/clones

Pick up a name for your repository, by example http://code.google.com/r/jeanderuelle-test-fork

The contributor then makes a local clone of their Google Code Project Hosting clone, which is stored on their local machine.
Instructions for checking it out is http://code.google.com/r/jeanderuelle-test-fork/source/checkout

The contributor creates a new Issue explaining their contribution at
http://code.google.com/p/sipservlets/issues/entry?template=Review%20request

The contributor then creates a new branch into their local clone

```
git checkout -b feature-branch
```

Do the changes into their branch for their local branch for the contribution and commit them

```
git commit -a -m "commit message"
```

_**IMPORTANT**:Please use the Google Code integration to use the commit message to tie the commits to the Issue you're working on. More information on that can be found at http://code.google.com/p/support/wiki/IssueTracker#Integration_with_version_control_

_**IMPORTANT**: When your change is pulled into the main Mobicents SIP Servlets source, the change description that you entered here will show up as changes in the main Mobicents SIP Servlets source, so please use a meaningful description - fixing bug, making changes, etc. are not ok, please instead use something like fixing transform bug caused by NPE, etc. so that it makes sense in the context of Mobicents SIP Servlets as a whole, not just your clone._

If you have any new files, make sure to use the following command before committing

```
git add <file or directory>
```

Same thing if you want to remove some files

```
git rm <file or directory>
```

## Pushing changes to your online clone ##

When a change is ready to be integrated back into the repository, that change is pushed from the developer's local clone to their Google Code Project Hosting clone.

```
git push origin feature-branch
```

To avoid merge soup, please rebase your branch first

#### Bringing in new changes from the upstream repository ####

If the main repository has evolved since your last push to your clone repository, you will need to bring those changes into your repository as well as potentially merge them.

You need to add a remote via which you will identify the upstream repository:

```
git remote add upstream https://code.google.com/p/sipservlets
```

Now whenever you want to merge upstream changes into your clone, do the following:

```
git fetch upstream
git merge upstream/master
```

#### Pushing changes to your clone repository ####

First pull in all of the latest changes from upstream, apply them to your master branch, then rebase your feature branch against master before merging it into master and pushing it upstream:

```
git checkout master
git fetch upstream
git merge upstream/master
git checkout awesome-feature
git rebase master
(fix any conflicts with upstream changes)
git push origin feature-branch
```

Browse to Source -> Changes from the project page for your clone and navigate to the page with details on the branch to be reviewed.
By example, http://code.google.com/r/jeanderuelle-test-fork/source/list?name=feature-branch

You will need to paste the URL for this page into the issue you created earlier.
Describe the code to be reviewed, its purpose, and paste in the URL for the relevant changeset(s) or branch(es).

The code will be reviewed on the contributor's clone - if any further changes are suggested, a couple of iterations might be needed so the contributor will need to modify the code again, commit, push and comment on the issue.

Once the change is approved, a committer of Mobicents SIP Servlets will merge it back into the main repository with the following commands.

```
git checkout -b feature-branch
git pull https://code.google.com/r/jeanderuelle-test-fork/ feature-branch
git checkout master
git merge feature-branch
```

Even though this may sound complicated, this process makes code reviews easier and allows a lot of people to work on changes in parallel.