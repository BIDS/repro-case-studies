##### Introduction
1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

Randy LeVeque, Professor of Applied Mathematics and one of the core developers of the open source [GeoClaw](http://www.geoclaw.org) software package for modeling tsunamis and other geophysical flows. Recently we have been using this software to study new approaches to probabalistic tsunami hazard assessement (PTHA), in which the goal is to take some probability distribution of possible future earthquakes that might cause large tsunamis and produce a probabilistic hazard map for a particular community, indicating which regions are most at risk and estimating the annual probability of flooding to a given depth at each point.  This is complicated by the fact that the depth of flooding by a particular hypothetical tsunami depends on whether it arrives at low tide or high tide, and we have developed ways to incorporate this uncertainty.

The workflow I will describe relates to a journal publication on this topic, which was based on work that was originally performed as part of a consulting contract funded by a private firm that was part of a broader pilot study funded by FEMA.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

There were two distinct aspects of reproducibility important in this work. The original development of new techniques was performed in the context of a project that went on for several years and required running many tsunami simulations with the GeoClaw code for the probabilistic studies, each of which took several hours of computing time and produced large quantities of output data.  During this time frame the GeoClaw software was evolving, along with our methodologies.  GeoClaw is openly developed on the GitHub site https://github.com/clawpack/geoclaw. We needed to be able to compare new results with those computed previously, and be able to identify what changed in the software or our code in between, if necessary.  For this aspect the goal was not to openly share all of our work or the results (nor were we allowed to, due to the nature of the project), but we needed to be able to reproduce results ourselves if necessary and keep the code under version control to identify changes.

The other aspect is that we wanted the particular new method written up in the journal paper to be accompanied by the Python code that implements the method and a sample set of data that was used to produce some of the figures in the paper.  In this context we wanted the figures to be reproducible by a reader using this code, in hopes that this would aid others in understanding the methodology and adapting the code to solve their own problems.


##### Workflow diagram


[Diagram](rjleveque.pdf)

##### Workflow narrative


We first created a new account on the UW campus computing system dedicated to this project that could be shared by the three collaborators, with sufficient storage for accumulating simulation results (and securely backed up by campus services).  On this account we created a Git repository that we could all access via ssh to use as our master repository for developing code, and eventually for writing the project reports.  We did not use GitHub since we wanted a private repository.  We did not use this repository for large datasets since these did not need to be under version control.  We archived some input data (such as the topography for the ocean and the coastal region being studied) on this account and wrote shell scripts to rsync this data to each collaborators laptop or other computers as needed. These scripts were kept in the Git repository.  Similarly we wrote scripts to rsync simulation results from the computer where the simulation was performed back to this account, along with some metadata.  The new methods being developed for tidal uncertainty were implemented in Python code used for postprocessing the simulation results.  One collaborator was doing most of the simulation runs, on several different computers, while another was developing and testing the postprocessing code, so rsync'ing the necessary data between laptops via the campus account was convenient as well as insuring that it results were archived as we went along.

The shared campus account was also used to host webpages so that the visualizations produced from each simulation could be viewed by all collaborators.  These webpages were also used eventually to share results with the project sponsors and reviewers of our preliminary report.

The private Git repository was also used for writing the final report in Latex and collecting the final figures to go into the report.  The third collaborator, who was less involved in the coding, was not completely comfortable with Git and so we also used Dropbox for sharing and commenting on drafts of the report, but all changes to the Latex were made in the Git version.

The final report was made available to the public by depositing it [in the UW ResearchWorks Archive](http://hdl.handle.net/1773/22366).

When we started working on the journal paper, we created a private Bitbucket Git repository for collecting the code specific to the paper and for the Latex file.  (We could have used the shared campus account for this as well; I am not sure why we switched to Bitbucket.) The submitted preprint was also posted [on the arXiv](http://arxiv.org/abs/1404.7216), so that it would be publically available.

The referees requested changes to the paper and some figures needed to be redone, which was easy to do since we had produced all figures with scripts in the Git repository.  The revised paper was developed in this same repository, along with the authors' responses to the referees.

After the revised paper was accepted by the journal, we created a new public GitHub repository for the code and small data sets needed to reproduce some of the figures in the paper that illustrated the basic methodology.  This repository was also linked to Zenodo, and a GitHub release was performed that triggered automatic archiving of a zip file of all the code at that stage, and assignment of a [DOI](http://dx.doi.org/10.5281/zenodo.12406).

In addition to the test problem for which we shared code, the final paper also contained some figures with results from the overall project, the probabilistic maps produced for Crescent City, CA using this methodology.  Reproducing these results would require running roughly 100 tsunami simulations.  We are fairly confident that we have all the code and data to reproduce these results if required, but we have not made this publicly available.

##### Pain points

  - Using rsync for large data sets worked fine once we figured out a good workflow and scripts, but is not ideal.  A version control system like Git that works well for large quantities of data would have been very useful.

  - Some data could not be shared and we also had to be careful about sharing preliminary results since emergency managers and the agencies involved are very sensitive about publicizing risk maps for specific communities before they have been properly vetted and agreed on.


##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

This workflow proved to be very valuable for this long-term project in which many parts of the code and methodology were evolving.  The initial project was followed by additional funding for a [Phase II](http://hdl.handle.net/1773/25916), in which the focus was on studying current velocities rather than only flow depth.  This required re-running all the tsunami simulations with a modified version of GeoClaw. Having done all the initial work via scripts archived under Git, it was relatively painless to redo these runs.  In the meantime other changes had also been made to the GeoClaw code, and having both our code and GeoClaw under version control was very useful when comparing results.

##### Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

For researchers who develop new methods and algorithms, it is often important to be able to see the details that are in the code but don't make it into the paper, both to better understand the work and to find potential errors.  It also facilitates comparing different methods for the same problem.

In natural hazards modeling, the simulation results may be used by engineers or policy makers to make decisions with public safety implications.  Transparency and reproducibiity are important aspects of accountability.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I became proficient with Git initially through involvement in open source software projects.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

  - Convincing collaborators to learn and use a common set of tools is sometimes a challenge, and some researchers are more willing to share code and data than others.

  - Some input data and/or results can not be shared publicly, so it may be necessary to selectively share data and perhaps have both private and public repositories. 
  
4) What do you view as the major incentives for doing reproducible research?

  - Ability to easily modify and build on past work.

  - Ability to compare new approaches or software with past versions and determine what changes made a difference in results.

  - Facilitates collaboration.

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

  - Using version control of some sort is the single most important first step.

  - Make a habit of cleaning up code used to produce final results so that it's well documented and all the necessary steps are clearly laid out. Then run through them from scratch if possible to insure that it works. Even if you don't plan to share it with others, your future self will thank you.

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

  - The UW eScience Institute Reproducibility and Open Science Working Group has developed [some guidelines](http://uwescience.github.io/reproducible/guidelines.html).

  - The 2012 [ICERM Workshop on Reproducibility in Computational and Experimental Mathematics](https://icerm.brown.edu/tw12-5-rcem/) resulted in a [final report](https://icerm.brown.edu/tw12-5-rcem/icerm_report.pdf) and [wiki](http://wiki.stodden.net/ICERM_Reproducibility_in_Computational_and_Experimental_Mathematics:_Readings_and_References) with recommendations and additional links.
