---
layout: episode
title: best practices
teaching: 20
exercises: 40
questions:
  - How can we collaborate with others within one repository?
objectives:
  - Understand how to collaborate using a centralized workflow.
  - Understand the difference between local branch, origin/branch, and remote branch.
keypoints:
  - Centralized workflow is often used for remote collaborative work.
  - "`origin` refers to where you cloned from (but you can relocate it)."
  - "`origin/mybranch` is a read-only pointer to branch `mybranch` on `origin`."
  - "These read-only pointers only move when you `git fetch`/`git pull` or `git push`."
---


Code reviews can be long, that is true, but just like any other process can be optimized. Here are some code review best practices that can be implemented in your company.

##  Techniques to ensure maximum efficiency

### Two reviewers are better than one
It’s not easy to find a consensus if there are two different opinions on the table and two people who have to agree on one of them. Despite how strict computer science can be, there are a ton of problems which solutions based on very non-scientific premises and guesses. Both sides can argue and even fight to prove one’s right. Not many developers have in mind business problems (time!), so they can waste a lot of resources on pointless discussions.

Another problem could be the personal character of team members. Sometimes people get frustrated because they can’t push opinion against someone with more communication skills.

To solve this problem, it only takes to introduce a third developer (typically second reviewer), who will tip the balance and eventually agree only with one of the parties (or propose another solution).

If you have the resources, I recommend having two reviewers by default, but if you lack developers time, add extra reviewer if there is a conflict to solve.

Worth to mention that some problems better fit specific issues. Typical developers pair can be more effective when summoning expert from a particular domain to audit the code.

So – try to have two reviewers or at least one backup reviewer.

### Make the Code Review a priority
Code review is a blocker for merging a feature, so if a developer requires some piece of code to be available for the new feature, it could be a problem. Required changes can be manually merged into the new feature before the start, but it can lead to code conflicts, on the other hand, the developer will wait to do nothing until changes are made.

As you know, blockers should be found as soon as possible and solved as quick as possible, so work is smooth as it gets.

So it is essential to make developers understand that pending code reviews (and overall pull requests) are actually more important than their own ongoing work (of course in a reasonable way, critical fixes are even more critical). It’s not an easy topic, because developers seem to care about their focus state a lot, but it can be communicated like this: make code review first thing developer do when:

Starting work in the morning
Going back from lunch
Going back from Fussball/PlayStation/darts break
Going back from meeting
So, if developers lose their focus anyway, make a habit first to check if there are no pending review by their peers.

Checking for new code review requests shouldn’t be too hard – it can be done in several ways. A developer can browse Github for open PRs with “Awaiting review from you” status. Also, each developer will probably get an email with a Code Review assignment. You can easily connect Github to Slack so that each open PR will be posted to the channel.

So – try to explain developers the importance of code review. Experiment with some rules to decrease code review waiting time.

### Establish Code Review rules and write them down
Code Review process, like any other process, can use some rules, especially in bigger and more complex projects. More developers in the team mean diverse experience and practices. It is good but sometimes can slow down the effectiveness of work.

So, each team should establish some set of rules and write them down (don’t miss this point!). I don’t think there is much benefit of standardizing process in a whole company, but the team works together on a daily basis. There are two significant benefits of making this happen:

New developer on the board requires education about existing rules. Don’t waste time on explaining every time the same things. It’s also frustrating to the new guy that he/she is corrected many times, instead of first reading how things are done in the team.
In case of conflicts or misunderstandings, there is a single, living source of truth which can be referenced.
Here are some code review best practices that I always include in my work, which can help you improve the code review process.

Only comment author can resolve comment – if code was corrected or after discussion author decides to fix it.
Don’t mention the same problem many times. Don’t bloat the code, say it once and ask to fix everywhere.
If there are pending, not resolved comments, the assignee is a code author who should fix or comment back.
If there are discussions commented by the code author, the assignee is reviewer, who should continue a discussion or resolve comments and approve.
Use labels to mark what actions should be next – e.g. “ready for review” “ready for the QA” etc.
The popular problem is when the code author thinks he/she is waiting for review, and the reviewer feels he/she is waiting for fixes/comments back.

So, establish some rules, write them down, and improve them over time.

### Ensure that Pull Requests are good
An inseparable part of code review is a pull request. The review is done on changes someone request to “pull” to the main branch.

If the PR is good, a code review should be easy and fast. If PR is bad – code review will be exhausting, long, and “no one will have time to do it.”

The main rule of good Pull Request is to keep it short. Two hundred lines of code are easy to understand and to find problems. Two thousand lines are not. The cognitive load increase is exponential relative to the number of changes done in the request.

Short PR can be checked during a coffee break – long PR will cost literally many hours, and code review quality will decrease because the reviewer will be eventually too tired and confused to keep quality for a long time.

An extra pro tip is to make PRs well labeled. An author should ensure request is linked to a ticket system (Jira etc.), and there is reasonable description/readme for reviewers.

So, ensure developers spend some little extra time to create a good quality pull request, which will return in many hours of reviewing work.

Introduce Code Review audits between teams
In large organizations with many teams and projects, there are, for sure, a lot of approaches on how to manage development teamwork. This is a great approach to improve!

More experienced team (e.g., with senior engineers) can naturally develop good practices based on their experience, even without any management help. This is an excellent opportunity to extend their workflow to other teams.

On the other hand, you can observe a team with aggressive comments, long waiting time, and a broken process. The faster you know it and fix it, the better. Don’t trust that things will escalate soon enough.

Think about performing periodic audits of selected teams to observe the condition of the code review process (just like your audit management, scrum meetings, etc.!). Some teams will have problems, and some will be outstanding. Use this knowledge to share the experience of developers and fix possible issues on the early stage.

So, think about assigning CTO or other senior-level engineer or technical manager to perform audits of daily development processes.

### Automate as much as possible
Developers prefer automating over manual and repetitive tasks. Code review might stand between code and human, but still, a lot can be delegated to the machine.

### Set CI pipelines
First of all, PR should trigger a CI pipeline with tests and builds. This step runs a few minutes and catches a lot of problems that might be detected by the reviewer. Well written tests should cover a lot of quality problems, but without set CI, someone can merge it even if tests fail.

Connect your CI pipeline tool to Github and block possibility to merge until all checks pass. Don’t waste developers’ time to check code which will not even build.

### Set code style formatters and linters
A lot of time wasted on code review is a ton of pointless comments related to tabs vs. spaces and how developers prefer code to be written (not what problems does it solve). Of course code consistency is important, but it shouldn’t bloat the code review process.

There are tools made to automate these jobs, like Prettier or ESLint for javascript ecosystem or Robocop for Ruby. They are responsible for applying and reporting about “code style guide” and practices I mentioned before. The more rules set, the more consistent, will be code. Developers can vote for changing existing rules or create new ones, but automated tasks will ensure that ongoing work is following existing ruleset.

I recommend setting code formatter automated on Git pre-commit hook (which will run automatically) and linters on Git pre-push hook (which will cancel push it doesn’t pass). Also, linter should run on the CI pipeline. When these checks pass, there is much less to check by reviewer, who can focus on problem-solving.

Deploy branch to test environment
If you have a decent time assigned to DevOps work, I recommend you to set automatic deployment of open Pull Requests. Typically if a developer wants to check if the code work, he/she has to download and build it locally. It takes time, and sometimes it’s also a problem – if the QA department or product owner wants to check new feature before the merge.

Preparing automatic deployments of PRs will cost time to set up, but will let the team quickly check ongoing work, also by non-technical people.

Extra pro-tips from Ideamotive Team
Commit often and publish work-in-progress PRs
There is a bad practice when some developers wait for days until they show some work. Encourage them to commit often and push frequently. It will not only save the work in case of losing code locally (theft, broken device), but it will make the team more productive. Opening “Work-in-progress” branch will allow others to check the overall concept of changes over monitoring the implementation. This is especially important for junior developers when a reviewer can say after a few lines of code that this is just a wrong direction. It’s better to remove 50 lines of code than 500 or (5000).

Favor reviewers who know the problem
Probably there is not much sense in asking frontend developer to check backend code. If the team is big enough to choose from reviewers, it’s an excellent way to improve code quality. Some developers will better understand domain knowledge; some of them will specialize in some narrow tech problems. They will better fit review where they can give a lot of valuable feedback.

Modern git services make this easier by detecting and suggesting relevant reviewers based on historical changes or code owners.

Set live meeting in case of significant changes
If Pull Request is huge (shouldn’t be, but it happens), it can cost a lot of time to ping-pong online discussion with hundreds of comments. In this case, it could be better to set up a desk meeting where the code author explains other changes.


## How to reduce conflicts during code review?
Code review, just like any discussion, could cause conflicts between developers. Also, it’s based on giving feedback, which is very hard for both reviewer (to do it with empathy) and author (to accept criticism).

Of course, the possibility of conflicts depends a lot on the individual character of developers, but if it happens, there are few rules, how to reduce it in the future.

Write down as much as possible
Conflicts can emerge when there are two different decisions, and parties don’t want to give up the idea.

However, a lot of decisions have been made already – but they are lost in time. I mentioned code style guide before – this is an excellent example because no one will argue about “tabs vs. spaces” if this has been officially decided and written in the project documentation.

There are different ways how to create documentation like this. I like tools like Notion to develop and maintain wiki-like pages with e.g., decisions made by business or rules established by developers.

Doc like this can be referenced during reviews to avoid unnecessary conflicts.




## Educate how to do a good Code Review
There are some rules about how code review should be performed to achieve its goals. Not every developer is aware of that.

The review should be based on facts, not guesses. It’s not a place to think about any personal matters – the only thing that matters is code change and how it affects the project.

Each comment with feedback should include the explanation (“this is wrong because”) and proposal of a better solution (“maybe try to do it like this: …”). Extra points for linking to external sources like documentation so that code author can learn for the future.

And the most important – developers have to understand that they have a common goal which is the best code they can do. This is not a place of personal ego or competition who is a better engineer.

## Introduce extra developer to solve conflicts
In case of ongoing conflict where there are two developers can’t agree with, you can invite the third developer to tip the scale and solve the problem. This extra engineer is not only an additional opinion but also a mediator between conflicted two.


## Centralized workflow

### Meaning of "central" in a distributed version control

![The GitHub Octocat]({{ site.baseurl }}/img/forking/github_octocat.jpeg)

Git implements a **distributed** version control.
This means that any type of repository links that you can think of can be
implemented - not just "everything connects to one central server".

In Git, all repositories are equivalent but we typically we consider one repository
as the main development line and this is marked as "central".
The "central" is a role, not a technical difference.

In this episode, we will explore the usage of a **centralized workflow** for collaborating online on a project
**within one repository**.


### Centralized layout

![]({{ site.baseurl }}/img/forking/centralized.svg)

Features:

- Typically all developers have both read and write permissions (double-headed arrows).
- Suited for cases where **all developers are in the same group or organization or project**.
- **Everybody who wants to contribute needs write access**.
- Good idea to write-protect the main branch (typically `master` or `main`).

Real life examples:

- Within the CodeRefinery team we mostly use this approach: [https://github.com/coderefinery](https://github.com/coderefinery)
- [https://github.com/ropensci/plotly](https://github.com/ropensci/plotly)

---

## Centralized workflow exercise

In this exercise we will practice collaborative centralized workflow in small
groups.  We'll discuss how this leads to code review and discuss a number of
typical pitfalls.


> ## Exercise preparation
>
> - We form small groups (4-5 persons).
> - Each group needs to appoint someone who will host the shared GitHub repository: *an administrator*.
> - For online teaching, use breakout rooms.
> - **One person per group (administrator)** generates a new repository
>   from the template [template-centralized-workflow-exercise](https://github.com/coderefinery/template-centralized-workflow-exercise)
>   called `centralized-workflow-exercise` (There is no need to tick *"Include all branches"* for this exercise):
> <img src="{{ site.baseurl }}/img/centralized/generate_repo.png" width="700"/>
>
> - Then **everyone in your group** needs their GitHub account to be added as collaborator to the exercise repository:
>   - Participants give their GitHub usernames to their chosen administrator (in their respective group, in online workshops you can use the Zoom chat for private communication within the breakout room).
>   - Administrator gives the other group members the newly created GitHub repository URL.
>   - Administrator adds participants as collaborators to their project (Settings → Manage Access → Invite a collaborator).
>   - Group members need to accept the invitation. GitHub emails you an invitation link, but if you don't receive it
>     you can go to your GitHub notifications in the top right corner. The administrator can also "copy invite link"
>     and share it within the group.
{: .prereq}

> ## Watching and unwatching repositories
>
> - Now that you are a collaborator, you get notified about new issues and pull
>   requests via email.
> - If you do not wish this, you can "unwatch" a repository (top of the project page).
> - However, we recommend watching repositories you are interested in. You can learn things from experts just by
>   watching the activity that come through.
{: .callout}

> ## Exercise description
>
> - Helper prepares an exercise repository (see above) - this will take 10 minutes or so.
> - The exercise group works on steps 1-8 (15-20 minutes).
> - After step 8 you can return to the main room. Please ask questions.
> - We do step 9 and 10 together (instructor demonstrates, and everybody follows along in their repositories).
> - Before we start with the exercise, instructor mentions all steps and explains what happens during a `git clone`.
{: .challenge}


#### 1. Clone your administrator's group repository

```
<!-- $ git clone {{ site.centralized_workflow_exercise_url }}.git centralized-workflow-exercise -->
<!-- ``` -->

<!-- Where you replace `coderefinery` by the namespace of the repository administrator. -->

<!-- Instead of using https you can also clone using ssh keys: -->
<!-- - [https://help.github.com/articles/connecting-to-github-with-ssh/](https://help.github.com/articles/connecting-to-github-with-ssh/) -->
<!-- - [https://docs.gitlab.com/ee/gitlab-basics/create-your-ssh-keys.html](https://docs.gitlab.com/ee/gitlab-basics/create-your-ssh-keys.html) -->

<!-- This is a representation of what happens when you clone: -->

<!-- *remote*: ![]({{ site.baseurl }}/img/centralized/01-remote.svg) -->

<!-- *local*: ![]({{ site.baseurl }}/img/centralized/01-local.svg) -->

<!-- > Here and in what follows, "c1" is a commit, "b1" etc. are commits on side branches -->
<!-- > and "m1" is a merge commit. -->

<!-- - We clone the entire history, all branches, all commits. In our case, we have one branch (we did not include *all branches* when creating our repository from template) and we have only one commit (*initial commit*). -->
<!-- - `git clone` creates pointers `origin/master` so you can see the branches of the origin. -->
<!-- - `origin` refers to where we cloned from, try: `git remote -v`. -->
<!-- - `origin` is a shortcut for the full URL. -->
<!-- - `origin/master` is a read-only pointer. -->
<!-- - They only move during `git pull` or `git fetch` or `git push`. -->
<!-- - Only `git pull` or `git fetch` or `git push` require network. -->
<!-- - All other operations are local operations. -->


<!-- #### 2. Step into the newly created directory -->

<!-- ``` -->
<!-- $ cd centralized-workflow-exercise -->
<!-- ``` -->

<!-- Try to find out where this repository was cloned from using `git remote -v`. -->


<!-- #### 3. Create a branch `yourname-somefeature` pointing at your commit -->

<!-- Create a branch from the current `master`: -->

<!-- ``` -->
<!-- $ git branch yourname-somefeature -->
<!-- $ git checkout yourname-somefeature -->
<!-- ``` -->

The `yourname-` prefix has no special meaning here (not like `origin/`): it is just part of a
branch name to indicate who made it.


#### 4. Create a file with a unique name, e.g.: `yourusername.txt`

In this file share your favourite cooking recipe or haiku or Git trick or whatever.


#### 5. Stage and commit the change

```
$ git add yourusername.txt
$ git commit
```

*remote*: ![]({{ site.baseurl }}/img/centralized/01-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)


#### 6. Push your change as a new branch

```
$ git push origin -u yourname-somefeature
```

Can we leave out the `-u`?


#### 7. Browse the network of branches and commits

After you have pushed your branch and other participants have too, browse the
network of branches and commits and discuss with others what you see.


#### 8. Submit a pull request

Submit a pull request from your branch towards the `master` branch.
Do this through the web interface.

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click". In a popular project, it means that anyone can
contribute with *almost no work* on the maintainer's side - a big win.


#### 9. Discuss and accept pull requests

**We do this step together on the main screen (in the main room)**. The instructor shows a submitted
pull request, discusses what features to look at, and how to discuss and review.

At the same time, helpers can review open pull requests from their exercises groups.

> ## Hint for breakout rooms
>
> If the helper in the room is the one who sets up the central repository, he/she
> cannot easily demostrate the steps via screen-sharing as the repository's owner. A
> good alternative is to have one of the learners screen-share and get advice on the
> steps from other learners and helpers!
{: .callout}

> ## Discussion
>
> ### Naming
>
> - In GitLab or BitBucket these are named **merge requests**, not **pull requests**.
> - Which one do you feel is more appropriate and in which
>   context? (The name **pull request** may make more sense in the forking workflow: next episode).
> - It can be useful to think of them as **change proposals**.
>
> ### Pull requests are from branch to branch
>
> - They originate from a source branch and are directed towards a branch.
> - Not from commit to branch.
> - Pull requests create new commits on the target branch.
> - They do not create new branches.
>
> ### Pull requests can be used for code review
>
> - Pull requests are like change proposals.
> - We recommend that pull requests are reviewed by someone else in your group.
> - In our example everyone has write access to the "central" repository.
>
> ### Code review and protected branches
>
> - A good setting is to make the `master` or `main` branch **protected** and all changes to it have to go
>   through code review.
> - Centralized workflow with protected branches is a good setup for many projects.
>
> ### Why code review
>
> - You see what others are working on
> - Collaborative learning
> - OK if students and junior researchers review senior researchers
> - Improves quality of the code
>
> ### Read more
>
> - This is a great resource: [Practical git PRs for small teams](https://scicomp.aalto.fi/scicomp/practical-git-prs/)
{: .discussion}

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/04-local.svg)

Finally also discuss {{ site.centralized_workflow_exercise_url }}/network.


#### 10. Update your local copy

Your branch `yourname-somefeature` is not needed anymore but more importantly, you need to sync your local copy:
Everybody needs to do this step in their exercise repository but we do this together in the main room
so that we can discuss this step and ask questions.

```
$ git checkout master
$ git pull origin master
```
*central*: ![]({{ site.baseurl }}/img/centralized/06-remote.svg)

*local*: ![]({{ site.baseurl }}/img/centralized/07-local.svg)

---

> ## (Optional) exercise or demo: Cross-referencing issues
>
> We will submit another change by a pull request but this time we will **first create an issue**.
>
> 1. Open an issue on GitHub and describe your idea for a change. This gives
>    others the chance to give feedback/suggestions. **Note the issue number**, you
>    will need it in step 3.
> 2. Create a new branch and switch to it.
> 3. On the new branch create a commit and in the commit message write what you
>    did, but also add that this "closes #1" (if the issue that you refer to had the number
>    1).
> 4. Push the branch and open a new pull request. If you forgot to refer to the
>    issue number in step 3, you can still refer to it in the pull request
>    form.
> 5. Note how now commits, pull requests, and issues can be cross-referenced by including `#NNN`.
> 6. Notice how after the pull request is merged, the issue gets automatically
>    closed.  This only happens certain keywords like `closes` or `fix`.
> 7. Discuss the value of cross-referencing them and of auto-closing issues
>    with commits or pull requests.
{: .challenge}


> ## Exercise/discussion: Why did we create a feature branch `yourname-somefeature`?
>
> This exercise is done in groups of 4-5 persons and can be done through a discussion only.
>
> Pushing directly to the main branch is perfectly fine for simple personal projects -
> the pull-request workflows covered here are for larger projects or for collaborative development.
> Guidelines for simpler workflows are given in the
> [how much git is necessary?](https://coderefinery.github.io/git-intro/14-level/) episode of the git-intro lesson.
>
> In collaborative development, whenever we update our repository we create a new branch
> and create a pull-request. Let's now imagine that everyone in your group makes a new change (create a new file)
> but without creating a new branch.
>
> 1. You all create a new file in the master branch, stage and commit your change locally.
> 2. Try to push the change to the upstream repository:
>
> ```
<!-- > $ git push origin master -->
<!-- > ``` -->
<!-- > You probably see something like this: -->
<!-- > -->
<!-- > ```shell -->
<!-- > $ git push -->
<!-- > To https://github.com/user/repo.git -->
<!-- >  ! [rejected]        master -> master (non-fast-forward) -->
<!-- > error: failed to push some refs to 'https://github.com/user/repo.git' -->
<!-- > To prevent you from losing history, non-fast-forward updates were rejected -->
<!-- > Merge the remote changes (e.g. 'git pull') before pushing again.  See the -->
<!-- > 'Note about fast-forwards' section of 'git push --help' for details. -->
<!-- > ``` -->
<!-- > -->
<!-- > - The push only worked for one participant. -->
<!-- > - Discuss why push for everybody else in this group was rejected? -->
<!-- > -->
<!-- > > ## Solution -->
<!-- > > -->
<!-- > > The push for everyone except one person fails because they are missing one -->
<!-- > > commit in their local repository that exists on the remote. They will first -->
<!-- > > need to pull the remote changes before pushing their own, which will usually -->
<!-- > > result in a merge commit. -->
<!-- > {: .solution} -->
<!-- {: .challenge} -->



<!-- > ## Discussion: How to make changes to remote branches -->
<!-- > -->
<!-- > We can create a local branch `somefeature` tracking `origin/somefeature`: -->
<!-- > -->
<!-- > ```shell -->
<!-- > $ git checkout -b somefeature origin/somefeature -->
<!-- > ``` -->
<!-- > -->
<!-- > If there is no local branch `somefeature` and there is a remote branch `origin/somefeature`, then this is enough: -->
<!-- > -->
<!-- > ```shell -->
<!-- > $ git checkout somefeature -->
<!-- > ``` -->
<!-- > -->
<!-- > The long form is only needed if you have multiple remotes containing a branch called `somefeature` -->
<!-- > (we will learn about multiple remotes in the next episode). -->
<!-- > -->
<!-- > Once we track a remote branch, we can pull from it and push to it: -->
<!-- > -->
<!-- > ```shell -->
<!-- > $ git pull origin somefeature -->
<!-- > $ git push origin somefeature -->
<!-- > ``` -->
<!-- > -->
<!-- > We can also delete remote branches: -->
<!-- > -->
<!-- > ```shell -->
<!-- > $ git push origin --delete somefeature -->
<!-- > ``` -->
<!-- {: .discussion} -->

> ## Creating pull requests from the command line
>
> There are several possibilties:
> - <https://cli.github.com/>
> - <https://hub.github.com/>
> - <https://github.com/NordicHPC/git-pr>
{: .callout}

> ## How you can find out in which repositories you are a collaborator
>
> Visit <https://github.com/settings/repositories> where you will see
> an overview of all repositories you have write access to.
{: .callout}

> ## GitHub/GitLab organizations
>
> - Projects often start under a personal namespace.
> - If you want the project to live beyond the interest or work time of one person,
>   one can share projects under an "organization".
> - You can then invite collaborators to an organization.
> - This is what we do in the CodeRefinery project: <https://github.com/coderefinery>
{: .callout}
