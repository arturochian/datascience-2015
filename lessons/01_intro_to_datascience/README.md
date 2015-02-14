# Objectives for today
- Establish high-level as well as concrete goals for the whole course
- Set up development environment
- Start coding

# Setting up our development environment
### Step 1: Download Sublime
- http://www.sublimetext.com/2

### Step 2: Create Sublime shortcut
- Open Terminal (also known as the command prompt in Microsoft Windows).
```
$ vi ~/.bash_profile
```
This will open your bash profile in Vim. To edit it, type i, then add this line:
```
export subl='open -a /Applications/Sublime\ Text.app/ $1'
```
Then quite the terminal and reopen it and execute the following line:
```
$ subl
```
and this should open up Sublime from the command line.
###

### Step 3: Create two folders under Development
- Create a Development folder:
```
$ cd
$ mkdir Development
$ cd Development
$ mkdir datascience
$ cd datascience
$ mkdir repos
$ mkdir vm
```
We've created a `Development` folder and within it a `datascience` folder.

Then within `datascience`, we have the `repos` folder which is where we will be writing and editing code. We also have the `vm` folder, which will house our virtual machine which will run the code we write.

### Step 4: Download and install VirtualBox

- Go to the [Virtualbox download page](https://www.virtualbox.org/wiki/Downloads) and download the appropriate binary. Open the binary and follow the installations instructions.

### Step 5: Download and install Vagrant

- Go the [Vagrant download page](http://www.vagrantup.com/downloads.html) and download the appropriate binary. Open the binary and follow the installations instructions.

### Step 6: Download and start the Data Science Toolbox
Next, run the following commands:
```
$ cd ~/Development/datascience/vm
$ vagrant init data-science-toolbox/dst
```

### Step 7: Edit our Vagrantfile
The previous step should have created a file called `Vagrantfile` in the `vm` directory.

Open it in Sublime and add these two lines to it near line 22

```
config.vm.network "forwarded_port", guest: 8888, host: 8888
config.vm.synced_folder "../datascience/repos", "/repos"
```

The first line allows to view iPython notebook in our browser when we run the notebook from the virtual machine.

The second line makes it so that we can edit code on our local computer using our favorite editor and have those changes automatically synced to our virtual machine where we will run the code.

Now let's create the machine according to the specifications in the Vagrantfile:
```
$ vagrant up
```

### Step 8: Log in (on Mac OS X and Linux)

- If you are running Mac OS X or some other UNIX-like operating system, you can log in to the Data Science Toolbox by simply running the following command in a terminal:

```
vagrant ssh
```

### Step 8: Log in (Windows)

- If you are running Microsoft Windows, you need to use a third-party application in order to log in to the Data Science Toolbox. We recommend **Putty** fvor this. Go to its [download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) and download `putty.exe`. Run `putty.exe` and enter the following values:

```
Host Name (or IP address): 127.0.0.1
Port: 2222
Connection type: SSH
```
(If you want, you can save these values as a session by clicking the "Save" button, so that you do not need to enter these values again.)

Next, click the "Open" button and enter "vagrant" for both the username and the password.

### Step 9: Install GA Data Science Bundle

- Run the following commands:

```
vagrant@data-science-toolbox:~$ dst update
vagrant@data-science-toolbox:~$ dst add gads
```
(Note that `vagrant@data-science-toolbox:~` indicates that this command should be run on the Data Science Toolbox.)

### Step 10: Set up IPython Notebook

Now that you are logged into your new virtual machine, invoke the following command to create a password-protected profile:

```
vagrant@data-science-toolbox:~$ dst setup base
```

Next, `$ exit` out of the virtual machine and use your favorite text editor to open up the `Vagrantfile` in the `MyDataScienceToolbox` directory. Uncomment and edit the line somewhere around line 22 to the following:

```
config.vm.network "forwarded_port", guest: 8888, host: 8888
```

This line instructs Vagrant to open up port 8888 so that the IPython Notebook server is accessible from your browser. Restart the Data Science Toolbox and log in again so that the changes take effect:

```
$ vagrant reload
$ vagrant ssh
```

To start the IPython Notebook server, run:

```sh
vagrant@data-science-toolbox:~$ sudo ipython notebook --profile=dst
```

- You can now access the IPython Notebook server at https://localhost:8888. Because the SSL certificate is self-signed, you may get a warning message from your browser. The image below shows how Chrome complains about this. Because you know what's on the server-side, you can just click on the "Proceed anyway" button.


# Practice
### Lab 1: Editing and running code
#### Objective: Learn to edit files on our local machine and run the code on the virtual machine
Add a file `test.py` to `~/Development/datascience/repos/` with the following two lines:
```
import pandas
print "We have pandas!"
```
and then login to the virtual machine using `vagrant ssh` and see that the new file is there under `repos` and then run that file using `python test.py`.

Try to run that same file outside of the virtual machine and just from `~/Development/datascience/repos` and see that it throws an error.

**Why does this happen?**

### Lab 2: Git workflow
#### Objective: Get comfortable with our work flow of solving problems and pushing to GitHub
Create a directory `~/Development/datascience/repos/dat-chapter-1`, initialize it as a git repository and push it to your own GitHub. Then add a README.md file with the following text:
```
Chapter 1 of GA Data Science 2015: Prove proficiency in Python and Pandas.
```
Then, commit the new file and push it to GitHub.

### Lab 3: Python starters
#### Objective: Warm up our python skills
Create a directory within `dat-chapter-1` called `labs` and within that create a directory called `exercise_1`.
As we always will do, within `exercise_1`, create a README.md with the following problem statement (feel to free use your own words)
```
My objective in doing this problem is to exercise my logic skills and practice for loops/list comprehensions.

PROBLEM: Write a function that takes a list of numbers `numbers` and
returns a sublist of `numbers` with only those numbers that are divisible by 33
or contains 2 as a digit.
```
Save the solution as `solution.py` under `exercise_1` and commit and push to GitHub.


# Homework: Push all of these to your GitHub
### Lab 4: `exercise_2`
#### Objective: Exercise those logic skills while building fluency in Python
Solve https://projecteuler.net/problem=2
Remember to write a nice problem statement and objective in the README.

### Lab 5: `exercise_3`
#### Objective: Learn to read data from a csv file and analyze it in pure Python
Using the `csv` library (https://docs.python.org/2/library/csv.html), read in this [data](https://www.dropbox.com/s/cbffxkqq0ujru58/rock.csv?dl=0) and answer the following 2 questions:

1. How many songs were released in 1981?
2. What are the top 20 songs by playcount? (Hint: use the built-in sorted() function, documentation here: https://wiki.python.org/moin/HowTo/Sorting)

**DO NOT open the file in Excel, otherwise you'll get some encoding errors.**
If you accidentally have opened it in Excel, delete and redownload.

### Lab 6: Go through Pandas Tutorial 1
### Objective: Familiarize ourselves with the basics of Pandas
Go through the following tutorial on your virtual machine, since it already has pandas installed.
This way, you'll feel more prepared for the next class, during which we'll delve deep into Pandas and start analyzing data..
- http://nbviewer.ipython.org/urls/bitbucket.org/hrojas/learn-pandas/raw/master/lessons/01%20-%20Lesson.ipynb

# Reading for next time
- [What is Numpy?](http://docs.scipy.org/doc/numpy/user/whatisnumpy.html)
- [5-min Tour of iPython notebook](http://ipython.org/notebook.html)
- [10-min Tour of Pandas](http://wesmckinney.com/blog/whirlwind-tour-of-pandas-in-10-minutes/)
