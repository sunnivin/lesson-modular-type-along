---
layout: episode
title: Modular exercise
teaching: 10
exercises: 45
questions:
  - Learn techniques for a generalized code development
  - What are the pros and cons of choosing a general code design?
objectives:
  - Do a modular based code development following a template
  - Get comfortable with the forking workflow
  - Write good commit messages
keypoints:
  - Experience difficulties in developing one-size-fit-all strategy
  - Repeat basic git-commands
  - Reflect on a typical development workflow in a small project
---

## Modular exercise with GitHub and Python
In this exercise, you will incrementally improve a python script for plotting some data together. It is a type-along/demo where we discuss and experience aspects of (un)modular code development. We will focus on the “why”, not on the “how”.

**NB** This exercise assumes that you are already familiar with how to use git as an individual or collaboratively through the web-interface. Because this is a slightly advanced lesson the commands you need to type during the exercise is deliberately not explicit for each step.

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

This example is in Python but we will try to see “through” the code and focus on the bigger picture and hopefully manage to imagine other languages in their place. For the Python experts: we will not see the most elegant Python.



---

> ## Exercise: modular type along with GitHub
>
> We will collaboratively develop a module based python code
>
> Objectives:
> - Repeat GitHub workflows (fork, commit, etc.)
> - Learn the advantages of modular based coding.
>
> Exercise:
> - **The exercise group works on steps A-F** (50 minutes).
> - Python3 and the libraries matplotlib and pandas need to be installed on your computer to run the example scripts.
{: .challenge}



### **Step A**: Clone and check

- Create a local clone of [this](https://github.com/sunnivin/module-based-type-along) repository.

- cd into the folder where the local repository is and create the branch `module-based-development`. Through all this exercise the variable $HOME is referring to the top folder of the repository.

- Run the initial python script from the $HOME folder:
``` shell
$ python src/initial.py
```

- Verify that the file `25.png` is created in $HOME.


### **Step B**: improve the plot
Your supervisor ask you to improve the plot by adding labels to the plot.

- Create a file `src/improvement.py` and add it to the repository.

- Add labels to the plot by adding the following lines to `improvement.py`:

``` python
import pandas as pd
from matplotlib import pyplot as plt


plt.xlabel('measurements')
plt.ylabel('air temperature (deg C)')


num_measurements = 25

# read data from file
data = pd.read_csv('data/temperatures.csv', nrows=num_measurements)
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

- Stage and commit the changes in `improvement.py`. You will be asked to do this in each step so you can inspect your (hopefully) beautiful log in the last step of the exercise.


### **Step C**: increase the number of plotted measurements
Your supervisor now tells you to make similar kinds of plots for 100 and 500 measurements as well. Since you know that code duplication should be avoided you decide to change the number of plots made of the measurements with a loop.

- Update `improvement.py` by copying in the following code.  The plots will now be generated with a for-loop over the variable `num_measurements`:

``` python
import pandas as pd
from matplotlib import pyplot as plt

plt.xlabel('measurements')
plt.ylabel('air temperature (deg C)')

for num_measurements in [25, 100, 500]:

    # read data from file
    data = pd.read_csv('data/temperatures.csv', nrows=num_measurements)
    temperatures = data['Air temperature (degC)']

    # compute statistics
    mean = sum(temperatures)/num_measurements

    # plot results
    plt.plot(temperatures, 'r-')
    plt.axhline(y=mean, color='b', linestyle='--')
    plt.savefig(str(num_measurements)+'.png')
    plt.clf()
```
- Run `improvement.py` again and verify that the files `25.png`, `100.png` and `500.png` are created. Why are the axis labels only present for the file `25.png`?

- Stage and commit the changes in `improvement.py`.


### **Step D**: abstracting the plotting part by introducing a function
A colleague advises you to abstract the plotting part into a function to divide the work into modules.

- Update the `improvement.py` file by copying the following code:

``` python
import pandas as pd
from matplotlib import pyplot as plt

def plot_temperatures(temperatures):
    plt.plot(temperatures, 'r-')
    plt.axhline(y=mean, color='b', linestyle='--')
    plt.xlabel('measurements')
    plt.ylabel('air temperature (deg C)')
    plt.savefig(str(num_measurements)+'.png')
    plt.clf()


for num_measurements in [25, 100, 500]:

    # read data from file
    data = pd.read_csv('data/temperatures.csv', nrows=num_measurements)
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
  - Do you see any problems with this solution? (Hint: what would happen if the functions in the file are copy-pasted into another file?)


- Run the modified `improvement.py` script.

- Stage and commit the changes in `improvement.py`.


### **Step E**: small improvements
After looking at the script you realize that you can functionalize all the parts of your script and use a for-loop.

- Update the `improvement.py` file by copying the following code:

``` python
import pandas as pd
from matplotlib import pyplot as plt


def plot_data(data, xlabel, ylabel):
    plt.plot(data, 'r-')
    plt.xlabel(xlabel)
    plt.ylabel(ylabel)
    plt.axhline(y=mean, color='b', linestyle='--')
    plt.savefig(str(num_measurements)+'.png')
    plt.clf()


def compute_statistics(data):
    mean = sum(data)/num_measurements
    return mean


def read_data(file_name, column):
    data = pd.read_csv(file_name, nrows=num_measurements)
    return data[column]


for num_measurements in [25, 100, 500]:

    temperatures = read_data(file_name='data/temperatures.csv', column='Air temperature (degC)')

    mean = compute_statistics(temperatures)

    plot_data(data=temperatures, xlabel='measurements', ylabel='air temperature (deg C)')
```
- **Wait for the other members of the break-out room and discuss this point**:
  - What will now happen if the functions are copy-pasted into another project/script? (Hint: how is for instance `num_measurements` declared?)

- Run the modified `improvement.py` script.

- Stage and commit the changes in `improvement.py`.



### **Step F**: improve to more stateless functions
After digesting the material in this workshop you realize that you can do one last effort of improving your script by making your functions more stateless (aiming for pure functions here!)

- Update the `improvement.py` file by copying the following code:

``` python
import pandas as pd
from matplotlib import pyplot as plt


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
        file_name="data/temperatures.csv",
        nrows=num_measurements,
        column="Air temperature (degC)",
    )

    mean = compute_mean(temperatures)

    plot_data(
        data=temperatures,
        mean=mean,
        xlabel="measurements",
        ylabel="air temperature (deg C)",
        file_name=str(num_measurements)+'.png',
    )
```

- Run the modified `improvement.py` script.

- Stage and commit the changes in `improvement.py`.

- Display your GitHub history and reflect around the comments you have written in  your log. Would you be able to follow the ideas of your history log if you were just reading the commit messages?
