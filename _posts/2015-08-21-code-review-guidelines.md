---
layout: post
title: "Code Review guidelines"
feature-img: assets/img/pexels/close-up-code.jpg
tags: [Code Review]
author-id: nettle
---

Rules and practical recommendations for Code Review with Gerrit:

* TOC
{:toc}

Submit your changes for review as early as possible
---------------------------------------------------

Sometimes it is important to get early feedback on your changes
especially if you are working on a big change, e.g. new feature.

Early feedback may change your mind on implementation approach and save your time.

Your colleagues will be aware of what and how you are doing,
it will be also easier for them to take your work over
in case of your unexpected absence.

> **Tip:** you can start from pushing a **Draft**:<br>
> `git push origin HEAD:refs/drafts/master`

Split your changes to smaller reviews
-------------------------------------

It is always easier and much faster to review smaller changes.

Large reviews tend to stuck for awhile because it is psychologically harder
to start analysis of big chunks of code.

Besides large reviews are usually not safe
since it is very difficult to check everything.

Always add Jira issue ref to commit message
-------------------------------------------

The first line of commit message should always look like: `[PROJ-XXXXX] Short summary`.

Never use `[task]`, `[WP:...]`, `[FIX:...]` etc in the first line of commit message,
add them in the detailed description.

Check your source code before submitting review
-----------------------------------------------

Run linters and static analyzers (`pep8`, `pylint`, `buildifier` etc) before submitting every patchset.

Reviewer should not run linters for you.

> **Tip:** install linter plugins/extensions in your code editor

Test your code before submitting review
---------------------------------------

Run all tests (unit, regression, consistensy, integration etc,
e.g. `python -m unittest discover`, `make test` etc),
before submitting every patchset.

Visually check patchset in Gerrit
---------------------------------

Before assigning **Reviewers** in Gerrit do a fast visual check of the changes
to spare others from the most simple mistakes.

Make sure that Gerrit displays the patchset correctly -
sometimes it might happen that you miss some small mistakes before "git push",
or Gerrit somehow corrupted your changes.

Meanwhile in Gerrit you see exactly what is going to be reviewed.

Always add **Assignee**
-----------------------

Never leave review unassigned.

**Assignee** is responsible for the review.

Always add all team members to **Reviewers**
--------------------------------------------

Your teammates should be aware of what you are doing.
They also can continue your work if needed.

Always write commit message and comments in English
---------------------------------------------------

English is a standard de facto for all kinds of internal documentation.

Always answer to the comments even if they are related to older patches
-----------------------------------------------------------------------

Feedback is important for your peer.

Show that you read a comment by saying e.g. `OK`, `Thanks!`, `I'll check it` etc

When you fixed the code, say `Fixed`, `Done` etc

> **Tip:** in Gerrit you can also mark a comment as `Done`
> by clicking corresponding button under comment panel

Be polite and write comments in friendly manner
-----------------------------------------------

* Always use **I-Message** technique:<br>
  say `I think ...`, `I would suggest ...`, `I guess ...` etc<br>
  instead of `Do this`, `Change that` etc
* Never use **You-Message**:<br>
  never say `You must ...`, `You are wrong ...`, `Your code is ...` etc<br>
* Ask questions instead of making statements:<br>
  say `What is the intention of ...?`, `Could you please clarify ...?`<br>
  instead of `This has no sense`, `This is wrong`
* Avoid the **Why** questions: `Why don't you ...?`
* Don't be rude: do not use `WTF?`, `What?` etc

Explain your point of view
--------------------------

Always explain why you suggest something even if you think it's obvious.
By doing so you spread knowledge but also make it possible to weigh pro and cons against each other.

Use prefixes in comments
------------------------
* `Critical:` to indicate a really important comment
* `Tip:` for tips and suggestions, sometimes alternative solutions
* `Nitpick:` comment might be useful but not much important

Do review as soon as possible
-----------------------------

Treat code reviews as a high priority.

If you can - start review immediately, if not - set it as the next item in your "to do" list.

Remember the author of changeset is waiting for your feedback,
sometimes he/she can be blocked by the review.

As the Author, do not hesitate to attract the Reviewer's attention by a "verbal ping",
e.g. during daily Standup Meeting.

Do not hurry up
---------------

Take your time while reviewing.

The most valuable feedback you can give is not about typos or indentation
but rater logical or structural problems.

Avoid Review stalemate
----------------------

Try to avoid stalemate by any means:

* Don't be stubborn, be always flexible.
* Never let your ego affect the Review. Never take it personal.
* Do not try to make everything perfect, remember - perfect is the enemy of good.

In case of `-1` or `-2` and the Author is not agree with that,
the Author or/and the Reviewer can involve one or more Reviewers
to resolve the situation via voting.

If the resulting review score is positive (at least `+1`) the proposed solution can live,
if negative (at least `-1`) - it should be reworked,
if zero - involve one more Reviewer etc.
