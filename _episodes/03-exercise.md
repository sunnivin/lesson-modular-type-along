---
layout: episode
title: python exercise
teaching: 10
exercises: 50
questions:
  - Learn techniques for generalizing code development
  - What are the pros and cons for chosing general code design?
objectives:
  - Know about pure functions (functions without side effects, functions which given same input always return same output).
  - Learn why and how to limit side effects of functions.
  - Get comfortable with the forking workflow.
keypoints:
  - Do a modular based code development following a template.
  - Experience difficulties in developing one-size-fit all strategy.
  - Repeat basic git-commands.
---

## Modular type along exercise with GitHub
In this exercise you will incremently improve a python script for plotting together. It is a type-along/demo where we discuss and experience aspects of (un)modular code development. We will focus on the “why”, not on the “how”.

### Data
The file temperatures.csv contains hourly air temperature measurements for the time range November 1, 2019 12:00 AM - November 30, 2019 11:59 PM for the observation station “Vantaa Helsinki-Vantaan lentoasema”.

Data obtained from https://en.ilmatieteenlaitos.fi/download-observations#!/ on 2019-12-09.

### Initial goal
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



### Our task

Our collaborators ask us to continue the code development to generalize the coding steps. Once we get this working for 25 measurements, our task changes to also plot the first 100 and the first 500 measurements in two additional plots.


Reflect around a typical development workflow in a small project. This example is in Python but we will try to see “through” the code and focus on the bigger picture and hopefully manage to imagine other languages in its place. For the Python experts: we will not see the most elegant Python.



---

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
> - Fork the helper's newly created repository and clone the fork so you can work on your global copy.
{: .prereq}

> ## Exercise: modular type along with GitHub
>
> We will collaboratively develop a module based python code
>
> Objectives:
> - Repeat GitHub workflows (fork, commit, etc.)
> - Learn the advantages of modular based coding.
>
> Exercise:
> - Helper prepares an exercise repository (see above; this will take 5-10 minutes).
> - **The exercise group works on steps A-F** (50 minutes).
> - After step F you can return to the main room. Please ask questions.
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
- Run the improved python script from the top folder in the repository:
``` shell
$ python src/improvement.py
```
- Verify that the axis are added in the file `25.png`.
- Stage and commit the changes in `imporvement.py`.


### **Step C**: increase the number of plotted measurements

- Your supervisor now tells you to make similar kind of plots for 100 and 500 measurements as well. To avoid code duplication you decide to change the number of plots made of the measurements with a loop.
- Update the `improvement.py` file by copying the following code with a `for`-loop over `num_measurements`:

``` python
import pandas as pd
from matplotlib import pyplot as plt

plt.xlabel('measurements')
plt.ylabel('air temperature (deg C)')

for num_measurements in [25, 100, 500]:

    # read data from file
    data = pd.read_csv('temperatures.csv', nrows=num_measurements)
    temperatures = data['Air temperature (degC)']

    # compute statistics
    mean = sum(temperatures)/num_measurements

    # plot results
    plt.plot(temperatures, 'r-')
    plt.axhline(y=mean, color='b', linestyle='--')
    plt.savefig(f'{num_measurements}.png')
    plt.clf()
```
- Run the modified `imporvement.py` script and verify that the files `25.png`, `50.png` and `100.png` are created.

- Stage and commit the changes in `imporvement.py`.


### **Step D**: abstracting the plotting part by introducing a function
- A colleague advice you to abstract the plotting part into a function to divide the work into modules.
- Update the `improvement.py` file by copying the following code:

``` python
import pandas as pd
from matplotlib import pyplot as plt

plt.xlabel('measurements')
plt.ylabel('air temperature (deg C)')


def plot_temperatures(temperatures):
    plt.plot(temperatures, 'r-')
    plt.axhline(y=mean, color='b', linestyle='--')
    plt.savefig(f'{num_measurements}.png')
    plt.clf()


for num_measurements in [25, 100, 500]:

    # read data from file
    data = pd.read_csv('temperatures.csv', nrows=num_measurements)
    temperatures = data['Air temperature (degC)']

    # compute statistics
    mean = sum(temperatures)/num_measurements

    # plot results
#   plt.plot(temperatures, 'r-')
#   plt.axhline(y=mean, color='b', linestyle='--')
#   plt.savefig(f'{num_measurements}.png')
#   plt.clf()
    plot_temperatures(temperatures)
```
- **Wait for the other members of the break-out room and discuss this point**:
  - What would we expect before running this code?  (Hint: how are the variables defined?)
  - Do you see any problems with this solution? (Hint: what would happen if the code is copy-pased into another file?)
- Run the modified `imporvement.py` script.

- Stage and commit the changes in `imporvement.py`.


### **Step E**: small improvements
- After looking at the script you realize that you can functionalize all the code parts of your script.

- Update the `improvement.py` file by copying the following code:

``` python
import pandas as pd
from matplotlib import pyplot as plt


def plot_data(data, xlabel, ylabel):
    plt.plot(data, 'r-')
    plt.xlabel(xlabel)
    plt.ylabel(ylabel)
    plt.axhline(y=mean, color='b', linestyle='--')
    plt.savefig(f'{num_measurements}.png')
    plt.clf()


def compute_statistics(data):
    mean = sum(data)/num_measurements
    return mean


def read_data(file_name, column):
    data = pd.read_csv(file_name, nrows=num_measurements)
    return data[column]


for num_measurements in [25, 100, 500]:

    temperatures = read_data(file_name='temperatures.csv', column='Air temperature (degC)')

    mean = compute_statistics(temperatures)

    plot_data(data=temperatures, xlabel='measurements', ylabel='air temperature (deg C)')
```
- **Wait for the other members of the break-out room and discuss this point**:
  - What will now happen if the functions are copy-pasted into another project/script? (Hint: how is for instance `num_measurements` declared?)

- Run the modified `imporvement.py` script.

- Stage and commit the changes in `imporvement.py`.



### **Step F**: improve to more stateless functions
- After digesting the material in the workshop you realize that you can do one last effort of improving your script by making your functions more stateless (aiming for pure functions here!)

- Update the `improvement.py` file by copying the following code:

``` python
import pandas as pd
from matplotlib import pyplot as plt
import click


def plot_data(data, mean, xlabel, ylabel, file_name):
    plt.plot(data, "r-")
    plt.xlabel(xlabel)
    plt.ylabel(ylabel)
    plt.axhline(y=mean, color="b", linestyle="--")
    plt.savefig(file_name)
    plt.clf()


def compute_mean(data):
    mean = sum(data) / len(data)
    return mean


def read_data(file_name, nrows, column):
    data = pd.read_csv(file_name, nrows=nrows)
    return data[column]


for num_measurements in [25, 100, 500]:

    temperatures = read_data(
        file_name="temperatures.csv",
        nrows=num_measurements,
        column="Air temperature (degC)",
    )

    mean = compute_mean(temperatures)

    plot_data(
        data=temperatures,
        mean=mean,
        xlabel="measurements",
        ylabel="air temperature (deg C)",
        file_name=f"{num_measurements}.png",
    )
```

- Run the modified `imporvement.py` script.

- Stage and commit the changes in `imporvement.py`.

- Display your GitHub history and reflect around the comments you have written in  your log. Can you follow the ideas of your development in the history log?


### **Step G**: pros and cons for module based code development
**We do this step together on the main screen (in the main room)**

Do we still agree on the initial points we wrote in the [HackMD](https://hackmd.io/GjKgLZ5jRYGPAbuPkCfGtw)?



#### Further improvements (we will see this tomorrow)
- Are there some obvious features we have not (yet) done in the file `imporvements.py`?
- If you are the supervisor of the student:  how would you suggest the student to perform the incremental imporvements? (Sneak-peak of the subject of tomorrow which is **code reviews**).
