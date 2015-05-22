##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Ben Marwick, and I am an Assistant Professor of archaeology in the Department of Anthropology at the University of Washington. My research interests include human-environment adaptations during the Pleistocene in Southeast Asia and Australia. My colleagues and I work with stone artefacts, organic and geological remains to understand past human behaviours and their environmental contexts.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In the context of this case study, reproducibility refers to computational reproducibility, which means enabling other people to combine the code and data that we produce to obtain the same statistical results and data visualizations that we present in our publication. I also expect that the code could be used for empirical reproducibility, where our code is applied to a new dataset to generate substantively similar results to our published results. 

##### Workflow diagram

My workflow diagram is enclosed as a PDF and also online here: 

https://drive.draw.io/#G0B06w3axv7XKTZW5UdksxMlZkYVU

##### Workflow narrative

Our project aimed to excavate a well-known archaeological site in northern Australia in an attempt to reproduce the findings of previous excavations in the 1990s that uncovered  controversial early evidence for human occupation of Australia. The project was initiated with a grant application written in Microsoft Word and circulated among the team by email.

The archaeological excavation was conducted with fairly standard modern techniques. These include a combination of direct digital capture of artefact and feature provenance with a total station, digital photography and GIS, and hand-written paper notes using structured site recording forms. These data from these forms was later entered into an Excel spreadsheet.

At the conclusion of fieldwork, post-excavation analysis continued at the home institutions of each of the team members. The tools for data collections and analysis at this stage were according to the norms of each lab, but the final products from this stage were MS Word and Excel files. At this point work began on a manuscript for publication, which was a MS Word document that was circulated among the authors by email.

As the specialist work concluded, the Excel and Word files were collected into an R Project using RStudio. The spreadsheets were converted to CSV files to ensure they could be accessed independent of any specific software. A research compendium was created, based on a custom R package. This package was written to contain custom functions used repeatedly in the analysis. The devtools package was used to develop the custom R package in RStudio. The testtools package was used to write tests to ensure the package functions performed as expected while they were being developed. An R markdown file was created as part of the compendium, and edited in RStudio to recompute and extend the analysis and visualizations from the specialist labs, and combine the key pieces of narrative text from the lab reports that contain statistical results. The R markdown file is a kind of lab note book where code and text are interwoven in a single document. It summarizes and extends the work of the team specialists using R script. The code in the R markdown file used several R packages, including dplyr and reshape2 for data cleaning and analysis, rioja and analogue for specialist environmental methods, and ggplot2 for visualization. The runtimes of the analyses are rarely longer than 30 min, so writing code and narrative, and testing are the most time consuming tasks here. 

The R package knitr and the pandoc program was used to execute the R markdown file to inspect the output as the code was being written. A docker container was created to create an isolated computational and portable environment for writing the R markdown document and developing the package. The docker image was backed up on the Docker Hub server, and tested using continuous integration from circle-ci.com  All of these components, data files, R markdown file, package files, etc. were all version controlled using Git locally and backed-up on a private repository at GitHub. One of the downsides of using the compendium approach is that the work is done by just a few of the team members because not everyone is familiar with the tools. 

While the analysis was being developed in the research compendium, a manuscript was being drafted in a MS Word document and circulated among the authors by email, and revised using track changes. The rendered output of R markdown document is also circulated among the authors by email and the manusrcipt is updated, and new ideas are incorporated into the analysis, and additional code is written, some code abandoned, new plots produced, and others deleted, etc. This is probably the messiest part of the workflow as it involves manual updating of the MS Word document with new values and figures from the rendered R markdown document, and two unrelated version control systems (Git and track-changes in MS Word). The non-linearity of the process is also a challenge as the authors negotiate how the manuscript and analysis should take shape.

As the review and updating cycle concludes, the manuscript is send for review by the Traditional Owners of the land where the archaeological site is located. After this review, which might involve some changes to the manuscript, the final draft is prepared for submission. At the same time, the GitHub repository that contains the research compendium is made public and continuous integration from travis-ci.com is added to monitor the effect of changes made during peer review. The compendium is also deposited at figshare.com and the persistent URL to the figshare repository is added to the text of the manuscript as a pointer to the data and code that generated the results and visualizations found in the paper. The MIT license is attached to the code, the CC0 license is attached to the data, and a CC-BY license is attached to the text. These licenses allow flexible reuse of our materials. The paper is then submitted for publication. At this point the data and software are openly available online for peer reviewers and others to inspect. The code includes the R package, which has documentation about installing the packages and using the functions, has unit tests, and has machine- and human- readable metadata about dependencies. We also make available the docker image that contains the compendium in an Linux environment so that all the dependencies external to R can be included in a single bundle. 


##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

Some of the pain points include:

- the inefficiencies of duplication of effort in translating the Excel-based analysis into R. This happens because only a few members of the team are familiar with R and related command line tools.

- the complexities of working on the draft manuscript and updating the analysis as the team explores different options and research directions. This places a requires the team members working on the research compendium to iterate quickly, and dis-empowers the other team members who are not familiar with R. 

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

##### Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

4) What do you view as the major incentives for doing reproducible research?

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?
