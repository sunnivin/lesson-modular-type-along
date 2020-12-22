---
layout: episode
title: python exercise
teaching: 10
exercises: 50
questions:
  - How can we generalize our code development?
  - Why should we design our code to be general ?
objectives:
  - Know about pure functions (functions without side effects, functions which given same input always return same output).
  - Learn why and how to limit side effects of functions.
  - Get comfortable with the forking workflow.
keypoints:
  - Do a modular based code development following a template
  - Experience difficulties in developing one-size-fit all
---

## Modular type along exercise with GitHub


## Our task
Reflect around a typical development workflow in a small project. This example is in Python but we will try to see “through” the code and focus on the bigger picture and hopefully manage to imagine other languages in its place. For the Python experts: we will not see the most elegant Python.

### Data

The file temperatures.csv contains hourly air temperature measurements for the time range November 1, 2019 12:00 AM - November 30, 2019 11:59 PM for the observation station “Vantaa Helsinki-Vantaan lentoasema”.

Data obtained from https://en.ilmatieteenlaitos.fi/download-observations#!/ on 2019-12-09.

## Initial goal
Our initial goal for this exercise is to plot a series of temperatures for 25 measurements and to compute and plot the arithmetic mean. We imagine that we assemble a working script from various StackOverflow recommendations and arrive at this answer:

``` python
import pandas as pd
from matplotlib import pyplot as plt

num_measurements = 25

# read data from file
data = pd.read_csv('temperatures.csv', nrows=num_measurements)
temperatures = data['Air temperature (degC)']

# compute statistics
mean = sum(temperatures)/num_measurements

# plot results
plt.plot(temperatures, 'r-')
plt.axhline(y=mean, color='b', linestyle='--')
plt.savefig('25.png')
plt.clf()
```


## Final goal
Our collaborators ask us to continue the code development to generalize the coding steps. Once we get this working for 25 measurements, our task changes to also plot the first 100 and the first 500 measurements in two additional plots.

---

<div class="alert alert-dismissible alert-warning">
  <button type="button" class="close" data-dismiss="alert">&times;</button>
  <h4 class="alert-heading">We will work with a new repository for this exercise!</h4>
  <p>
    For this exercise we will fork a different repository compared to earlier today.
    Please step out of the repository and check that you fork the <b>forking</b>-workflow-exercise.
  </p>
</div>


> ## Exercise preparation
>
> **Helpers in breakout-rooms**:
> - Create an exercise repository by
>   [generating from a template](https://help.github.com/en/articles/creating-a-repository-from-a-template)
>   using this template: <https://github.com/sunnivin/module-based-type-along>
> - In this case we **do not add collaborators** to the repository (this is the point of this example).
> - Share the link to the newly created repository in the shared document with your group.
>
> **Learners in breakout-rooms**:
> - Fork the helper's newly created repository and clone the fork.
{: .prereq}

> ## Exercise: practice collaborative forking workflow
>
> We will collaboratively develop a module based python code
>
> Objectives:
> - Repeat how to fork and modify the fork.
> - Learn the advantages with modular based coding.
>
> Exercise:
> - Helper prepares an exercise repository (see above; this will take 5-10 minutes).
> - **The exercise group works on steps A-E** (15-20 minutes).
> - After step E you can return to the main room. Please ask questions.
> - **We do step F and G together** (instructor demonstrates, and everybody follows along in their repositories).
> - If there is a lot of time left, step G can be done back in an exercise room.
{: .challenge}



### **Step A**: Fork and clone


Wait for the helper to share the repository for this exercise in the group chat.
- Fork the helper's repository and  create a local clone.
- cd into the folder where the local repository is and create the branch `module-based-development`.
- Run the initial python script from the top folder in the repository:
``` shell
$ python src/initial.py
```

- Verify that the file 25.png is created in your top folder.


### **Step B**: improve the plot
Your supervisor ask you to improve the plot by adding labels to the plot.

- Create the file `src/improvement.py` and add it to the repository.
- Add labels to the plot by adding the following lines to `improvement.py`:

``` python
import pandas as pd
from matplotlib import pyplot as plt


plt.xlabel('measurements')
plt.ylabel('air temperature (deg C)')


num_measurements = 25

# read data from file
data = pd.read_csv('temperatures.csv', nrows=num_measurements)
temperatures = data['Air temperature (degC)']

# compute statistics
mean = sum(temperatures)/num_measurements

# plot results
plt.plot(temperatures, 'r-')
plt.axhline(y=mean, color='b', linestyle='--')
plt.savefig('25.png')
plt.clf()
```
- Verify that the axis are added in the file `25.png`. Stage the changes in `imporvement.py`.


### **Step C**: increase the number of plotted measurements

Before we do any modification, we create a new branch and switch to it: this is
a good reflex and a good practice. Choose a branch name which is descriptive of
its content.

On the new branch create a new file which will hold your recipe,
for instance `traditional_coderefinery_tacos.md` (but change the name). You can get inspired
[here](https://github.com/sinker/tacofancy/tree/master/full_tacos). Hopefully we all use different
file names, otherwise we will experience conflicts later (which is also interesting!).

There is also a file called `test.py` which will automatically verify whether your recipe contains the string
"taco" (case insensitive). This is there to slowly introduce us to automated testing.

Once you are happy with your recipe, commit the change and in your commit
message reference the issue which you have opened earlier with "this is my
commit message; closes #N" (use a more descriptive message and replace N by the
actual issue number).

And here is a picture of what just happened:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-02.svg)


### Step D: Push your changes to the fork

Now push your new branch to your fork. Your branch is probably called something else than "feature". Also verify where
"origin" points to.

```shell
$ git push origin feature
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-03.svg)


### Step E: File a pull request

Then file a pull request from the branch on your fork towards the master branch on the repository where you forked from.

Here is a pictorial representation for parts D and E:

![]({{ site.baseurl }}/img/forking/forking-2.svg)

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click".

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-03.svg)

Wait here until we integrate all pull requests into the central repo
together on the big screen.

Observe how the issues automatically close after the pull requests are merged
(provided the commit messages contain [the right keywords](https://help.github.com/en/articles/closing-issues-using-keywords)).

> ## (Optional) Exercise: try to send a conflicting pull request
>
> If you complete parts A-E much earlier than others, try to send another pull request
> where you anticipate a conflict with your first pull request.
{: .challenge}

> ## (Optional) Exercise: practice making changes to your pull request
>
> You can do that by pushing new commits to the branch where you sent the pull
> request from. Observe how they end up added to your pull request.
{: .challenge}


### Step F: Discuss and accept pull requests

**We do this step together on the main screen (in the main room)**. The instructor shows a submitted
pull request, discusses what features to look at, and how to discuss and review.

At the same time, helpers can review open pull requests from their exercises groups.


### Step G: Update your fork

We do this part **after the contributions from all participants have been integrated**.

Once this is done, practice to update your forked repo with the upstream
changes and verify that you got the files created by other participants.

Make sure that the contributions from other participants are not only on your local repository
but really also end up in your fork.

Here is a pictorial representation of this part:

![]({{ site.baseurl }}/img/forking/forking-3.svg)

We will discuss two solutions:


#### Longer route

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?
- Replace below with the repository you forked, if needed

```shell
$ git remote add upstream {{ site.forking_workflow_exercise_url }}.git
$ git fetch upstream
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-04.svg)

```shell
$ git checkout master
$ git merge upstream/master
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-05.svg)

```shell
$ git push origin master
```

*central*: ![]({{ site.baseurl }}/img/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/forking/github-remote-04.svg)

*local*: ![]({{ site.baseurl }}/img/forking/github-local-06.svg)


#### Shorter route

Remotes are aliases. We can use remote URLs directly.

Here we pull from the central repo and push to our fork
(replace with the repository you forked if needed):

```shell
$ git checkout master
$ git pull {{ site.forking_workflow_exercise_url }}.git master
$ git push https://github.com/user/forking-workflow-exercise.git master
```

> ## (Optional) Exercise: squash merge a pull request
>
> If you complete this exercise much earlier than others, pair up with somebody,
> create a new repository, fork it, and send a pull request with several
> small commits. On the other computer accept these with "Squash and merge" and later compare the source
> and target repositories/branches how they differ after the small commits got squashed into one.
{: .challenge}

---

<br>
<br>
<br>
![]({{ site.baseurl }}/img/forking/remote.jpg)
## Luke Skywalker: *You know, I did feel something. I could almost see the remote.*

## Ben Kenobi: *That's good. You've taken your first step into a larger world.*

(from Star Wars Episode IV - A New Hope)

---

> ## Discussion: Always create a feature branch
>
> - Never commit to the branch you wish to submit the pull request towards.
> - For each pull request create a new branch.
>
> Motivation:
> - Limits the risk that commits get accidentally appended to an open pull request.
> - History-rewrite (rebased and/or squashed commits) on the central repository does not lead to a diverging local default branch.
>
> See also [this
> blogpost](https://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/)
> for an explanation.
{: .discussion}
