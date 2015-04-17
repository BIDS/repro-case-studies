##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Justin Kitzes, and I am a quantitative ecologist who develops theory and models to predict the effects of land use and climate change on biodiversity. I am currently a postdoc in the Energy and Resources Group and a Data Science Fellow in the Institute for Data Science at the University of California, Berkeley.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

I consider a study to be (computationally) reproducible when I can send a colleague a zip file containing my raw data and code and he or she can push a single button to create all of the results, tables, and figures in my analysis. It can, of course, be quite challenging to achieve this goal with anything short of the simplest scientific workflows.

##### Workflow diagram

[Diagram](jkitzes.pdf)

##### Workflow narrative

This study investigated whether several common species of bats showed decreased activity near three large highways around San Francisco Bay. Activity in this study was defined as the number of ultrasonic foraging calls recorded by autonomous acoustic detectors. The core analysis tasks involved collecting raw call data using the detectors, extracting features of the recorded calls, classifying the calls to the species level, and performing statistical analysis on the resulting nightly call counts as a function of predictor variables, including distance from the road. The final analysis was published in PLoS ONE (doi:10.1371/journal.pone.0096341).

Two different types of detectors were used, one of which recorded data in zero-crossing format and the other in full spectrum format. The full spectrum data was converted to zero-crossing using a closed-source utility provided by the detector manufacturer, with conversion parameters selected to produce output similar to the recordings from the native zero-crossing detector. The free, closed-source software AnalookW, developed by an individual researcher who has been active for many years in bat call analysis, was used to filter out files containing only noise and, for the remaining calls, extract twelve features describing from each call. These features were saved in a csv table.

The calls were then classified by species, which required the construction of a custom random forest classifier. A reference library containing zero-crossing calls made by individual bats identified in hand was obtained from a personal contact, and the same twelve features were extracted for these calls using AnalookW. A random forest classifier was trained on this data using the Python package scikit-learn v0.12. Classifier accuracy was evaluated using cross validation and a confusion matrix.

The classifier was then applied to identify the recorded calls to the species level, creating a classified call table. This table was summarized into a nightly pass table, which aggregated the calls into passes consisting of multiple, closely spaced calls, and counted the number of passes of each species recorded in each night, at each distance from the road. Environmental and site variables were joined to this pass data to create the final table for statistical analysis.

As functions for fitting generalized linear mixed models (GLMMs) were not available in Python, statistical analysis was carried out in R. Exploratory analysis showed that a Poisson regression was not appropriate for the data, so a negative binomial GLMM was fit to the nightly counts of all species and separately for four common species. The model results were saved as a table that later appeared in the final manuscript. The model result table was then read by a Python script, which created and saved several figures, one of which appeared in the final manuscript. The final manuscript was written in LaTeX and submitted to journals in that format.

In addition to the manuscript, this analysis also led to the creation of the open source software BatID, which bundled the classifier object with a web-based GUI to enable non-programmers to classify California bat calls using a similar workflow to the one presented here.

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*

At the beginning of the pipeline, two graphical programs had to be used, one to convert a proprietary data format to the zero-crossing format and the second (AnalookW) to perform feature extraction on the zero-crossing calls. Both of these steps required parameters to be entered into these programs, which I was careful to document manually, as this information can otherwise easily be lost. AnalookW runs only on Windows, which required me (and any analysts wishing to use my later software BatID) to locate a Windows computer to complete this step. Although I code faster and more accurately in Python, I needed to switch to R for statistical analysis, as the necessary packages were not (and still are not) available for Python. A major headache at the manuscript stage arose because the R statistical functions reported output only as a non-machine-readable text file or as an object, which required me to create the final table, containing coefficients and standard errors for 14 variables across 5 models, by hand.

Once I created and released the BatID software, a problem immediately arose when scikit-learn updated to v0.13, which could not read the classifier object created during my analysis. Additionally, the original BatID package required a user to install a full scientific Python stack, a task that proved difficult for precisely the audience of non-programmers that I was hoping to reach. I eventually used pyinstaller to create a standalone binary executable for Windows, reasoning that users of the software needed a Windows computer anyway in order to run AnalookW as a prior step in the analysis.

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want ahem to learn from your example?*

Of all aspects of the analysis, I am particularly happy about the effort that I put in to creating the BatID standalone classifier software. As the majority of my colleagues in ecology are non-programmers or novice programmers, I believe that these types of user-friendly tools are critical to advancing the state of science in my field, as well as the uptake of new methods by non-academic non-profit and agency scientists, and I hope that more of my computationally-oriented colleagues will engage in similar activities in the future.

Ironically, of course, in creating a tool for non-programmers, I also created another graphical program that cannot easily be scripted into a workflow such as the one. I attempted to ameliorate this concern in the most recent BatID version by requiring users create a text file containing all parameters, which is read by the program along with the data file, and having the program save all results in the same directory as the parameter file, along with a log file. This at least ensures that there is, by default, some record of the program version, time, and parameters used to process the raw data into classified results tables.

##### Key tools [Optional]
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience.*

[Answer, 200-400 words]

##### General questions about reproducibility [Optional]

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

I think that reproducibility is particularly important in fields like ecology in which researchers are constantly striving to make increasingly detailed inference and predictions using relatively scarce data. Although I do not have evidence to this effect, it seems logical to me that in these "high leverage" types of analyses, small analytical decisions (how data are cleaned, the options passed to optimizers, etc.) could play a disproportionate role in influencing the eventual study outcomes, and thus need to be fully documented and shared. An easy way to guarantee that all of these decisions are recorded is to make one's entire analysis reproducible by others. More broadly, I feel strongly that reproducibility is a basic component of good science. Now that "doing science" requires communicating more detail than can be easily expressed in narrative form in a manuscript, releasing code and data seems completely necessary across all domains.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I started learning these tools through workshops, in particular Josh Bloom's Python bootcamp and through teaching Software Carpentry bootcamps with other experienced instructors. I also learned a great deal by working closely with Chloe Lewis, a former student in my PhD lab who had previously worked at Microsoft, on the development of our software package _macroeco_, which I continue to maintain. I picked up more advanced techniques and ideas mostly through web searches while attempting to get unstuck from issues that arose in my own research and software development.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

A major challenge in ecology continues to be data sharing and access. Many field ecologists, understandably, are reluctant to share their hard-won raw data with other researchers. I suspect that this caution arises both from a sense of professional necessity (i.e., I invested a ton of time collecting this data and I am going to be the one to publish all of the analyses using it) and from the feeling that the numbers alone cannot possibly capture all the subtle nuances they observed in the field that are important to truly understanding the data, its potential, and its limitations. In particular, information about sampling bias (as derived from choices of study site, sampling techniques, season, missing data, and many other factors) cannot easily be described in numeric form -- I also suspect that many field ecologists believe that it's not even in the manuscript, implying, very unfortunately for reproducibility, that the person who collected the data is the only one qualified to analyze it. What data is published and available tends to be relatively small and of heterogeneous format, and thus tends to be locked up in printed pdf tables and other non-machine-readable formats.

4) What do you view as the major incentives for doing reproducible research?

I'm not sure that there are any major external incentives in my field -- certainly, in principle, releasing reproducible research could increase the number of researchers who end up citing your manuscript, but this seems somewhat indirect. Some journals, like PLoS, are now mandating that all novel computer code be uploaded as manuscript SI, but it seems that this requirement is not particularly thoroughly checked.

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

[Answer]

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

[Answer]
