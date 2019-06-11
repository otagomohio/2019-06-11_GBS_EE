
# Introduction to the command line

## Getting on the supercomputer

During this session, we will learn to be comfortable with the command line. First, we will log in to the server [Mahuika](https://support.nesi.org.nz/hc/en-gb/articles/360000163575-Mahuika), a computing resource maintained by the New Zealand eScience Infrastructure (NeSI). 

You might have managed to log in to NeSI already. If you have not, please request help from one of us and we will assist you.

Next, we will hop across to the bit of Mahuika we are using for this workshop using (note, the `l` following `v` is a lower case "L" not a one!):
```
ssh -Y ga-vl01
```

Once you have jumped on to `ga-vl01` using the commands above, get into the space created for you for this workshop by using the `cd` (change directory) command (don't worry - we are going to go through commands like `cd` in more detail in a sec!):

```
cd /nesi/nobackup/nesi02659/users/<yourusername>
```

NeSI has a ton of different projects for a bunch of researchers around the motu (country). The project we are using for this workshop is `nesi02659`. You might notice `nesi02659` is in the "path" shown in the `cd` command above. We are going to cover paths to files and folders in just a minute!


## Introduction to the command line

For this session, we will use material created under a Creative Commons license by The Carpentries. [The Carpentries](https://docs.carpentries.org/index.html) teaches foundational coding and data science skills to researchers worldwide. The Carpentries is active in New Zealand and @Otago, we encourage you to keep your eyes open for [local events](https://otagocarpentries.github.io/).

We will go through the following carpentries lessons together:

* [Navigating Files and Directories](https://swcarpentry.github.io/shell-novice/02-filedir/index.html)
* [Working With Files and Directories](https://swcarpentry.github.io/shell-novice/03-create/index.html)
* [Pipes and Filters](https://swcarpentry.github.io/shell-novice/04-pipefilter/index.html)
* [Finding things](https://swcarpentry.github.io/shell-novice/07-find/index.html)
* [Loops](https://swcarpentry.github.io/shell-novice/05-loop/index.html) (if we have time)


## Let's practice what we just learned!

We have now gone through the basics of the command line. Let's reinforce some of what we just learnt in this [final exercise](bashgenomics.md).


## Additional resources

Learning the command line might seem hard at first but it gets a lot easier with a little bit of practice! As well as the resources we just covered, here are a few more to help you out if you get stuck:
* [Codecademy](https://www.codecademy.com/learn/learn-the-command-line)
* [Linux Cheatsheet](http://cheatsheetworld.com/programming/unix-linux-cheat-sheet/)

If you learn better in person with other folks, please check out the events run by Otago Carpentries, Otago Study Group, and Otago Mohio (a South Campus spin-off of Otago Study Group):
* [The Carpentries](https://otagocarpentries.github.io/)
* [Otago Study Group](http://otagostudygroup.github.io/studyGroup/)
* [Otago Mohio](https://otagomohio.github.io/)




[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
