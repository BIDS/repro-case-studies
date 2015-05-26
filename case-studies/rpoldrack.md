##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Russell Poldrack, and I am a professor in the Department of Psychology at Stanford University.  My work uses neuroimaging, genomics, and behavioral studies to examine the brain systems involved in decision making and executive control.  Many of our workflows use high-performance computing due to the large data and complex nature of the workflows.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In the context of my case study, "reproducibility" means the ability to exactly reproduce the analysis workflow that was used to obtain the results reported in a manuscript. More generally, I take the term to also emcompass the consistency of results across different workflows or datasets. 

##### Workflow diagram

poldrack.pdf

##### Workflow narrative

Referring to your diagram, describe your workflow for this specific project, from soup to nuts. Imagine walking a friend or a colleague through the basic steps, paying particular attention to links between steps. Don't forget to include "messy parts", loops, aborted efforts, and failures.

This workflow is meant to outline the analysis of a complex dataset including neuroimaging, behavioral, transcriptomic, and metabolomic data (http://www.myconnectome.org).  The data were collected over the course of 18 months from a single individual, and will be made fully available online upon publication of the manuscript via the OpenFMRI project (http://openfmri.org/ds000031).  The data are released under a public domain dedication, meaning that anyone can do anything they wish with the data, with no restrictions on redistribution or requirements of attribution.  I chose this approach because I feel that it will provide greatest degree of utility for the data.

The data processing stream was initially built in a non-reproducible manner on a single laptop.  After completing this, I became interested in generating a reproducible version of the workflow so that other researchers can exactly reproduce the analyses. A challenge of reproducible analysis in this study is that the raw data are very large (several TB including the raw genomic and neuroimaging data).  These data are being made available to any who wishes to use them, but it is not possible to easily provide reproducible workflows for these operations because they require large-scale supercomputing resources. For the processes that require supercomputing (such as genome alignment for RNA-sequencing data and surface-based parcellation for MRI data), we have shared most of the code used to complete these workflows.  Another complication of full reproducibility is that some of the preprocessing operations were performed by another laboratory, using code that they are not currently willing to share openly. Thus, we made the decision to focus on building an open reproducible workflow that encompasses as much as possible of the processing stream, using preprocessed data downloaded from an online archive.

The goal of this process was to create a completed automated analysis stream that requires no manual intervention.  The workflow uses a number of tools, including python, R, MATLAB, and the Connectome Workbench.  I started by generating scripts to perform each of the operations, but ultimately decided to generate a single python package to coordinate the entire workflow (available at https://github.com/poldrack/myconnectome)  .  The first operation of this package is to download the preprocessed data from Amazon S3, using the boto package in python.  We then perform additional processing of each of the different data types.  For the neuroimaging data, this is primarily performed using a set of python functions to extract and summarize connectivity measures between different brain regions.  For the transcriptome and metabolomic data, this is performed using a set of Rmarkdown scripts executed using R. The outcomes of each of these analyses are saved and used to compute timeseries correlations between each of the measures across all domains (for a total of more than 20,000 statistical tests), using the R forecast package.  These are then summarized in a web report generated using Rmarkdown.  Currently the only test is one that compares the results of the full workflow to a set of results cached on S3.  Documentation of the code is minimal.

After implementing the workflow on a single system, I then implemented it on a virtual machine in order to allow anyone anywhere to run it.  I used the Vagrant software package to provision a virtual machine with all necessary requirements.  Once installed, the user can run the entire workflow with a single command.  Documentation for installing and running the software is evolving.


##### Pain points
A few pain points:
- Extra work generalizing the code to work on an arbitrary system (primarily the identification of dependencies)
- Concern about exposure of errors or poor coding.
- What is the right technology for sharing a reproducible workflow?  We have used a VM provisioned using Vagrant, but there are many other approaches that one might use.
- What is the level of user at whom we are targeting this?  It's a lot of work to make it easy to use for non-power-users.


##### Key benefits
- Provides a degree of detail that could not be feasibly included in the publication.
- Increases the degree of trust amongst others in the field in one's results
- Provides an example for others in our subfield of how to implement reproducible shared workflows.

##### Key tools

I have used Vagrant (https://www.vagrantup.com/) to allow any user to easily provision a virtual machine that includes all of the necesssary dependencies to run the workflow (see https://github.com/poldrack/myconnectome-vm).

##### General questions about reproducibility


1) Why do you think that reproducibility in your domain is important?

The workflows used for neuroimaging data are highly complex with a great degree of analytic flexibility, which raises concerns regarding the reproducibility of results.  We desperately need a greater degree of transparency in order to make research in our domain more reproducible.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I think I primarily learned from negative examples; that is, from seeing other researchers whose research findings rely upon code that is not openly available and data that are not shared.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

- Human subjects issues and concerns about scooping are often raised here, but I think these are red herrings.
- The primary pitfall is that reproducible research practices make it harder to obtain splashy findings that get high-profile publications.  

4) What do you view as the major incentives for doing reproducible research?

- trust in one's research

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

- version control
- data sharing


6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?
