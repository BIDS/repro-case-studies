##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Chris Gorgolewski and I work at Stanford University in the department of Psychology. My field of research can be broadly characterized as Human Cognitive Neuroimaging. In layman words we are trying to related observed human behavior to neuronal processes in the brain. 

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

Reproducibility means an accurate description of experimental methodology and accessibility of tools used during the course of the study. Reproducibility is important when looking for mistakes and when attempting replications.

##### Workflow diagram

![](cgorgolewski_diagram.png)

##### Workflow narrative

The goal of this study was to relate the content and the form of self generated thought (mind wandering) to the dynamics of brain activity at rest. It was based on a publicly available data collected at the Nathan Kline Institute in collaboration with Child Mind Institute (data is available [here](http://fcon_1000.projects.nitrc.org/indi/enhanced/)). Three major aspects of this study makes it reproducible

* Data is publicly available.
* Scripts to run the analysis depend on freely available software and are also publicly available.
* Results has not only been described in a [paper](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0097176), but are also available in a machine readable way.

Feature extraction (data preprocessing - everything done before fitting a model) in neuroimaging can be a complicated process involving many different components. We have written our pipelines using the [Nipype](http://nipy.org/nipype) framework that allows researchers to combine many different well tested neuroimaging tools into one pipeline. The pipeline was tested and developed on a single subjects and then run on all subjects using a local supercomputer. Neuroimaging pipelines have been deposited at [github.com](https://github.com/NeuroanatomyAndConnectivity/pipelines/tree/master/src/mindwandering).

Behavioral data have been analyzed using R and knitr package providing reproducible reports that include narrative, code and figures. The R code, input behavioral data, outputs of the analysis (factors extracted from the questionnaire) as well as the questionnaire used for the study have been deposited on [github.com](https://github.com/NeuroanatomyAndConnectivity/NYC-Q).

Final version of all the analyses were fully automated, but the data required semiautomated quality control. Analysis has been done by one person within 3 months. Three other researchers consulted on the project.

Unfortunately no tests have been written for the data analysis software. The documentation also did not extend beyond comments and knitr reports.

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

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
