##### Introduction

1) Who are you and what is your research field? Include your name, affiliation,
discipline, and the background or context of your overall research that is
necessary specifically to introduce your specific case study. 

My name is Ariel Rokem. I am a Data Scientist at the University of Washington eScience Institute. My research training and experience have mostly been in the field of human cognitive neuroscience. During my postdoctoral training (2011-2015) in Brian Wandell's group, in the Department of Psychology at Stanford University, I conducted studies of human brain structure and function. A focus of my research is the application of ideas from statistical learning theory to measurements of human white matter with diffusion MRI (dMRI). 
The project described here evolved from a question that often arises in many fields of science: what measurements should I make? And given the measurements I am making, what model should I use for my data? Measurements of dMRI are used by scientists as a way to assess the structure of the human brain and its connectivity *in vivo*. There are many parameters of the measurement that are determined by the experimenter. For example, the duration of the application of magnetic field gradients during the scan affects the sensitivity of the measurement to subtle variations in diffusivity. On the other hand, it has a detrimental effect on SNR. Similar trade-offs apply to spatial resolution, scan duration, etc. The field had been developing models of the white matter based on different measurements, but there was no extensive study of the fits of these models to the data, and no assessment of the effects of these measurement parameters on the model fits, and the inferences that can be made.
In the study described here, we used cross-validation to evaulate two commonly used models in a variety of measurements.
The work was eventually published in [PLoS One](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0123272)

2) Define what the term "reproducibility" means to you generally and/or in the
particular context of your case study. 

Reproducibility is the public availability of code and data, such that only a reasonable effort would be required to generate the evidence (numbers and visuals) used to support a scientific finding. It is a matter of degree.  Ideally, a small number of commands at a shell
prompt would suffice, but in some complex cases, more work could be required. Even then, no more than copying of the data, and installation of software dependencies should be needed before the issuing of only a small number of commands  would be required to produce the evidence suppoting a scientific claim.  Some findings require large amounts of data storage, or large amounts of computation.  Reproducibility is a matter of degree, not of kind. 
A higher standard, sometimes called 'replicability' would be to require that the same conclusions be reached if another group of researchers were to do the same experiments, and implement the same ideas in their analysis. Reproducibility does not guarantee replicability (Leek and Peng, 2015). Again, it is understood that there are degrees of variation between reproducibility and replicability, that depend on the scientific question.


##### Workflow diagram

arokem.pdf


##### Workflow narrative

The project started with the collection of a data-set of MRI scans. Two subjects were scanned in several different experimental conditions. Each scan was repeated twice, to create a test-retest data-set. An additional four subjects were also scanned for another study in the lab (Takemura et al. 2015), in one of the conditions for another study, and their data was incorporated into the analysis, during review, to address comments about sample size. 

All data were collected in the MRI scanner at the Stanford Center for Neurobiological Imaging (CNI). The CNI has developed a scientific data management system called NIMS or SDM [Wandell et al. 2015], which captures the data from the scanner, archives it, and exposes a web interface, allowing researchers to control access to the data, and copy it into the lab's storage, a RAID system. 

The data were preprocessed using a series of *standard* steps. These are standard in the sense that any practitioner of MRI would perform these steps on his or her data, for example correction of motion artifacts and alignment to a common coordinate frame. These steps were only performed once, at the beginning of the study, except when visual examination of the results of these steps revealed an error. The code that performs these steps is part of the lab code distribution, [`vistasoft`](https://github.com/vistalab/vistasoft), which is version-controlled and freely available through github. These preprocessing step also takes advantage of publicly available code from other labs, which complicates dependency handling, because as these libraries evolve, the results of these steps might change, and affect the outcomes of subsequent steps.  

All analysis subsequent to preprocessing was done using a set of python modules that I developed in a git/github repository called [`osmosis`](https://github.com/vistalab/osmosis). This included implementations of many methods for fitting the data, statistical analysis and visualization, as well as utility functions for handling data analysis tasks, and utlity functions handling parallel execution on Stanford's `proclus` HPC cluster.  Much of the module code was covered by unit tests, and a few end-to-end tests of some of the model fitting procedures were implemented to track when regressions occured. Thus, many of the steps in the implementation of the analysis were run on a daily basis, during the development of the project. Testing was often a time-consuming affair. For many of the directions that did not pan out, the setting up of tests seems in retrospect to have been time misspent. On the other hand, some subtle issues did arise as a result of this testing. 

One of the problems that I encountered early in the development of the project was that some of the model fitting methods were rather time-consuming (hours), including several steps. While model evaluation required model fitting, it would not require that it be repeated every time an evaluation is made. To deal with this, I implemented caching mechanisms in the software that would store model fit parameters on disk, as needed. A major problem that arises from this caching mechanism is that as model fitting code evolved, it is hard to tell whether cached parameters are up-to-date with the current state of the code. When in doubt, model fits had to be rerun, and the cached results were overwritten.

Scripts using the module code were developed using the IPython notebook. When generally useful functions would emerge in the interactive work with the notebook, these functions would be copied into the modules.  

As the project evolved a few of these were copied into a [documentation folder](https://github.com/vistalab/osmosis/tree/master/doc/paper_figures)

A benefit of working with IPython notebooks is that running a basic notebook server on the lab compute server allowed me to take advantage of relatively powerful compute resources from the browser window on my latpop. 

Eventually, we copied the preprocessed data that we used to a data repository hosted by the Stanford libraries. This repository provides permanent URLs (PURLs) to the data, which we have used in papers. These PURLs can also be used to cite the data. Most of the data was licensed under the Creative Commons Atttribution licens, but some small amount of data was released under the Public Domain Dedication License, for use as part of the Dipy software (which has a non-restrictive BSD license). The software in osmosis was also released under an attribution license.

Because it records the evolution of scientific ideas, the `osmosis` code-base contains many dead ends and directions that did not work out.  During the work on this project, I became involved in an open-source project, which develops software for the analysis of dMRI data in python: [Dipy](http://dipy.org). Eventually, as the project matured, I started porting some of the ideas into Dipy. Mostly, these were reimplementations of software that was implemented in `osmosis`. This is because some of the APIs did not match, and a better understanding of some of the underlying issues. 

The `osmosis` repository continued to serve us in development of a couple of other projects in the lab. Specifically, one of the research students in the lab contributed code to extend the previous ideas to other. I ended up porting some of these ideas into  the Dipy code-base as well. Thus, some of the ideas became polished and the 


* For each part of that workflow:

    * How often does this step in the workflow happen?

    * How long does it take?

    * Which members of your team participate (or not)?

    * How much human intervention is involved?

        * Is that human intervention recorded in some way?

    * How much is scripted or otherwise automated?

        * What records are kept about this automation process?

    * Which software or online tools do you rely on?

        * What are its key important uses and limitations?

        * Does it make you more efficient or slow you down?

        * Does this tool affect your ability to reproduce your results?

        * Have you previously tried any other tools for this task?

        * Are you aware of tools that might make this step more efficient? If so, why have those tools not made it into your workflow?

    * How opaque is this step to a researcher external to your research group?

        * Is the necessary code online?

            * How is the documentation?

            * Are there tests?

            * Do you keep example input files alongside your code?

        * Is your raw data online?

            * Is it citeable?

            * Does the license allow external researchers to publish a replication/confirmation of your published work?

        * Is your data processing workflow online?

            * Are the scripts documented?

            * Would an external researcher know what order to run them in?

            * Would they know what parameters to use?

[Answer, 500-800 words]

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*




[Answer, 200-400 words]

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example?*

[Answer, 200-400 words]

##### Key tools [Optional]
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience.*

[Answer, 200-400 words]

##### General questions about reproducibility [Optional]

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

[Answer]

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

[Answer]

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

[Answer]

4) What do you view as the major incentives for doing reproducible research?

[Answer]

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

[Answer]

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

[Answer]


##### References 

J.T. Leek and R.D. Peng (2015). Opinion: Reproducible research can still be wrong: Adopting a prevention approach. PNAS 112: 1645-1646

B. A. Wandell, A. Rokem, L. M. Perry, G. Schaefer, R. F. Dougherty (2015). Data management to support reproducible research. arXiv:1502.06900v1

H. Takemura, A. Rokem, J. Winawer, J.D. Yeatman, B.A. Wandell, F. Pestilli (2015) A Major Human White Matter Pathway Between Dorsal and Ventral Visual Cortex. Cerebral Cortex, DOI: 10.1093/cercor/bhv064 pdf.

A. Rokem, J. Yeatman, F. Pestilli, K.N. Kay, A. Mezer, S. van der Walt, B.A. Wandell (2015). Evaluating the accuracy of diffusion MRI models in white matter. PLoS One, DOI: 10.1371/journal.pone.0123272.