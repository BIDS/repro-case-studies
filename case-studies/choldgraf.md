##### Introduction
1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Chris Holdgraf, I am a 4th year graduate student with the Helen Wills Neuroscience Institute at UC Berkeley. My thesis work involves using predictive models to understand how auditory regions of the brain respond to acoustic features. Specifically, I am interested in how experience, learning, and assumptions about the world shape the way that we interact with low level features. This involves a lot of computational work and coding, utilizing a number of packages in the python scientific ecosystem.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

The discussion in this writeup covers the first 6 months of the project. To that extent, my definition of "reproducibility" would actually being able to reproduce my own results (aka, coding for my future self). I ran into a lot of issues with keep things streamlined and understandable in my own head, which made it difficult to interpret my findings. Obviously this would generalize to other scientists trying to reproduce my analyses and work as well.

##### Workflow diagram

See attached.

##### Workflow narrative
My workflow involves taking raw data from lots of different sources, doing a few steps of munging on each one separately, combining them into a common structured format, and then doing further processing on this data. Here's a general breakdown:

Wrangling raw data
---
The raw data for my work involves electrophysiology signals collected from the brains of surgical patients all across the country. This is challenging because the nature of the data is quite different from one location to another. I often get the neural data in many different formats, and a loose collection of metadata (e.g., sensor locations, names, sampling rates) that can be anything from a PDF of hand-written notes to a structured text file. As such, the first step in my workflow is to wrangle all of this data into some kind of structured format.
First, I put all data into subject-specific folders. Each of these folders has sub-folders for different kinds of data (e.g., "raw", "munged", "meta"). The sub-folders will eventually be populated with data during processing, and the structure is consistent across all subjects so that I can easily parse them with scripts.
Next, I have an ipython notebook that is unique for each person I get data from. This is called "munge_subject_name.ipynb", and will output a file that I can then use for the rest of my analyses. The reason I use an ipython notebook here is that each subject is different, and will require a different set of steps to munge the data well. For this reason, I like to have lots of plots that go along with the analysis process, and a record of exactly what code was run to create the munged data for that subject.
Because the data often comes in different formats, I make the munging notebook output the same format for everyone. In this case, it is a "Raw" file using the mne-python toolbox. This is a great package for neural analysis in python, because it can write and read "fif" files, which are also readable in matlab (another common language for neuroscience). The output files are stored in the folder "s_name/munged"
The last thing I need to do in this step is take the metadata files that are unique to this subject, double check that all the values inside are correct (this is done with the munging notebook), and then insert them into a "combined" csv file of metadata for all subjects that I have. I have a python script called "create_combined_meta.py" that will look through all the subject folders, find the metadata files that my munging notebook outputs, and turn them all into a single CSV file. I can then query this CSV file as I would a database using Pandas. This simplifies things, because it means that while I have a separate file for each dataset, I have a single combined file across all subjects for their metadata.

Cleaning the data
---
Once I've created my munged data, I can now use a single script for processing/analyzing all data sets. In my field, there is a common set of standard preprocessing techniques that are carried out in order to improve the quality of the data (e.g., a few filtering steps). I have a "clean_data.py" file that will look through the "munged" folder of each subject, load the data, run the cleaning, and then output the results to the folder "s_name/clean". This way, I know that any data in the clean folder is ready for further analysis.
At this point, I have cleaned data in each subject's folder, I also have that subject's metadata inserted into a CSV file with all subject information. From now on, I can just load a subject's data file, then load the metadata CSV file for everybody, and query only the rows that belong to the subject that I care about.

Extracting Features
---
The next step in my analysis often involves extracting some features for a particular project I'm working on. At this point, I will create a new project-specific folder that exists alongside my "data" folder. The project folder is structured similarly to the "data" folder, but with scripts, sub-folders for data, etc that are unique to this project, rather than subject-specific.
The first thing I do is create some python script to extract features of interest for this project, I will put it in "project_name/script/extract_feature.py". This script assumes that there is data in the "clean" folder for each subject. It will pull the data from "clean", extract whatever feature I'm interested in, and then save the result to the project-specific folder, so something like "project_name/data/my_feature/{subject_name}_feature.fif". I  parse all subject folders and save files in the same manner.
Now, for this particular project I have the data of all subjects in a single project-specific data folder. This makes it much easier to develop scripts/notebooks to further analyze the results, since I don't need to keep track of which features have been extracted for which subjects. I also often develop feature extraction scripts to utilize things like the sun-grid engine, because this step often takes a long time to complete. I can do this relatively easily because the folder structure for each subject is the same.

Running analyses
---
Now that I have a set of features created for each subject, it is time to run analyses and answer questions. These scripts also exist in the project-specific folder, and assume that there is data in the "project_name/data/my_feature" folder. The scripts are often in ipython notebook format, because I often prefer to analyze this data interactively. I may prototype an analysis, and then turn it into an SGE python script if the analysis takes a particularly long time. The outputs of this analysis then go into a "project_name/results/my_analysis" folder. They may be in the form of PDFs and SVGs for further inspection, or data files (e.g., HDF5) representing model results (such as regression coefficients).
Finally, I can use the outputs of the analysis script to create visualizations and decide whether or not anything actually worked. I will use another notebook to read in the data in the latest "results" folder, perform last-second wrangling, statistics, etc. And output visualizations and so-forth. If I have a publication-ready figure in mind, I will create a notebook specifically for that figure in another folder called "project_name/fig". This is where I will spend more time making the plots look pretty, arranging many of them into a single figure, and finally outputting to SVG. Finally, I use microsoft word to write drafts which I put in the "doc" folder. These pull from the figures I've created in the "fig" folder. Ideally I would use text files here w/ latex, but the people I work with makes this prohibitive.

A general note
---
This is a process that has been refined many times over the past year, and the original structure looked very different than this. My original file system had code and data living in totally different places. Moreover, it had project-specific scripts and more general utility scripts living in the same place. The goal of this file structure is to keep data and scripts together when they are more-or-less paired with one another anyway, and to separate out my more production-ready functions/modules from my hackier project-specific scripts. Below is a list of some things that I've learned along the way, and that have guided the development of this system:

1. For any data and code that are project-specific, keep these together in the same general file hierarchy.
1. Rather than creating metadata structures that live next to the data, come up with a “master” metadata template, then store entries from every subject in a CSV file that follows this template. Rather than storing data in separate subject files, include an entry with “subject id” in the metadata file so that I can pull out individual subjects in this way.
1. Utilize other packages whenever possible, particularly with the annoying task of data I/O. In my case, I am now storing all my raw data as ‘.fiff’ files, which can be opened easily in python or Matlab with well-supported third party packages. I am also using pandas to read / write metadata files, which makes it very easy to slice and dice these files for particular entries that I want.
1. More generally, take a “database” approach to how I store any data. Even though I’m not storing data in a MySQL database per-se, I can still draw inspiration for how this data is organized. Treat data entries as rows, and data features as columns, and then combine / split up the data using pandas database-style syntax (e.g., joins and merges)
1. Put ad-hoc code in my project-specific folder. Be much more picky about code that I decide to expose as a part of my more general collection of python modules that work for any project. If I do think a function is worth generalizing, then move it out of the project folder and to its proper module, and document it extensively.
1. Do all of my coding with automatic PEP8 and PEP257 checkers (this is quite easy with sublime text). Fix any errors that come up in my general python modules.
1. Make a conscious effort to structure python scripts differently from ipython notebooks. Structure my code (and data) such that it lends itself well to scripting, rather than assuming interactive sessions for everything.
1.Use ipython notebooks to quickly take glances at the data and preliminary analysis results, but quickly move code into scripts as it becomes more refined. This avoids creating a mega notebook with tons of different analyses in it.
1. Structure my code so that some scripts live with the data that they operate on. E.g., if I’ve got a script that only takes raw data, renames specific columns in that data, and always saves it to another location relative to the original data, then create another folder “script” right next to my raw data folder. Put all scripts for the raw data into this folder. This way, I know that scripts operate with relevant data nearby.
1. Finally, this is not specific to this project but has been very useful to me. Find opportunities to contribute to other open-source projects. Open pull requests and learn about how to use the code. The back-and-forths and input you get will make you a much better coder, and your codebase / research will greatly benefit from it. 

##### Pain points
The hardest part of my workflows has been to decide how to balance flexibility and control. On the one hand, you don't want your scripts to be so specific to data that they break as soon as anything changes, but on the other hand creating code that generalizes well and isn't terribly confusing is really difficult to do. In my case, I basically made errors on both of these sides at first, but the current structure of my data seems to be more intuitive, easy to maintain, and easy to grow.
Another big issue I've had with reproducible workflows like the one I've described above is in dealing with different kinds of data/information. For example, I want to version control all of the code that I write, but does that mean that I should create one big repository for all of the code described above? What about a separate repository for each project? How should I split up the general sets of modules and functions vs. the code that only lives with a particular project? And finally, how should I deal with the fact that there are lots of other non-code files living with this file structure? Should they be version-controlled, or should the code just assume that the data lives in particular folders? What would happen if somebody else copied the code and didn't get the data? I don't necessarily have good answers for these issues, and I'm still coming up with a solution that makes me happy for the aforementioned structure, but these are some things that I'm thinking about.

##### Key benefits
I think that the biggest benefit of this system is in the fact that messy, subject-specific data is quickly turned into a standardized format that is consistent across everybody. This is useful because it means that you can write scripts that analyze the entire dataset without doing a lot of extra customization. Moreover, because the structure of the filesystem is the same for everybody (including things like naming conventions), it is easy to find what you want from each data set.
Another benefit is the fact that I am storing code along with the data that it operates on. Some people feel strongly that this is a bad idea, but I've found it to be useful so long as the within-project folder structure still makes sense. In previous workflows, I had all of my code in one folder, and all of my data in another folder. This often led to confusions where I was unsure which code operated on what data. It also made it more difficult to connect the steps of preprocessing and feature extraction chains. Now, I know that if I want to know all of the kinds of things that have been done to a collection of data files, I generally just need to look into its corresponding "script" folder.
Finally, by separating out operations that are true for all projects (e.g., data munging and cleaning) and those that are project-specific, the scope of individual projects becomes more clear and easy to follow. I think of the data pipeline as a single trunk, where projects branch out from this trunk and do extra things to the data, on top of the base workflow of preprocessing. Now, my file structure more naturally follows this concept.

##### Key tools [Optional]
The two most useful tools that I have found are Pandas and MNE-python. Pandas made it much easier to embed metadata with the signals that I was analyzing. It allowed me to store information from lots of subjects in a single CSV file, and treat it as a "database" by using queries on it. MNE-python is a package for electrophysiology in neuroscience written in python. When I discovered it, I realized that it duplicated many of the functions I had already written, and in general did this much better than I did. Moreover, it had a lot of convenience functions for doing I/O, which up until then was a pain to maintain. By using these two packages, I was able to significantly cut down on the amount of custom-written functions that I used to wrangle my data.

##### General questions about reproducibility [Optional]

1) Why do you think that reproducibility in your domain is important?

Because it's a guiding principle that will make my code more understandable, maintainable, and extendable for others and for myself.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

At first it came from teaching a few software carpentry classes and reading things online. Lately, I have gotten a lot of help by contributing to the MNE-python project, as I've found that going through the pull request process for a well-maintained project is a great way to learn a lot about coding well.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

In my case, legality is a big problem because I'm dealing with medical data that cannot be shared publicly. Another big problem is simply a matter of training and incentive. Right now there is little opportunity to learn how to code well or how to make reproducible science. To make matters worse, I see very little incentive for anyone to actually do so.

4) What do you view as the major incentives for doing reproducible research?

Other than the warm fuzzy feeling, I think the biggest advantage is that when you code and organize for other people, you also code/organize for yourself in the future. This makes your life much easier in the long run.

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

Front-load a lot of thinking/planning before you just start creating scripts and functions. Spend a good chunk of time at the start thinking "big picture", then zooming in and building some stuff, then zooming back out and deciding if it was a good idea or not. Don't get lost in the weeds.

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

software carpentry is a great one, but most other stuff is just scattered on stack overflow unfortunately. I think that finding a good package that has a sweet-spot of contributors (aka, not so few that you don't get feedback, not so many that it's a huge PITA to do anything) and trying to contribute something via a pull request will be a great way to learn good coding principles.
