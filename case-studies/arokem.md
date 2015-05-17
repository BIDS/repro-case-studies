##### Introduction

1) Who are you and what is your research field? Include your name, affiliation,
discipline, and the background or context of your overall research that is
necessary specifically to introduce your specific case study. 

My name is Ariel Rokem. I am a Data Scientist at the University of Washington eScience Institute. My research training and experience have been mostly in the field of human cognitive neuroscience. During my postdoctoral training (2011-2015) in Brian Wandell's group, in the Department of Psychology at Stanford University, I conducted studies of human brain structure and function, using quantitative MRI. A focus of my research during that time was the application of ideas from statistical learning theory to measurements of human white matter with diffusion MRI (dMRI). 

2) Define what the term "reproducibility" means to you generally and/or in the
particular context of your case study. 

Reproducibility is a matter of degree, not of kind. It usually depends on the availability of code and data from a scientific study, such that only a reasonable effort would be required to generate the evidence (numbers and visuals) used to support a scientific finding.  

Ideally, a small number of commands at a shell prompt would suffice, but in some complex cases, more work could be required. A reasonable amount of effort required might be rather extensive, when large amounts of data storage, or large amounts of computation are needed.

A higher standard, sometimes called 'replicability' would be to require that the same conclusions be reached if another group of researchers were to do the same experiments, and implement the same ideas in their analysis. 

Reproducibility does not guarantee replicability [Leek and Peng, 2015]. Some may even argue that reproducibility and replicability may sometimes be in conflict, because implementation errors can be propagated in reproduction, but not in replication [citation needed].

##### Workflow diagram

[Diagram](arokem.pdf)

##### Workflow narrative

Measurements of dMRI are used as a way to assess the structure of the human brain and its connectivity *in vivo*. Many parameters of the measurement are determined by the experimenter, and incur trade-offs between sensitivity and SNR. Models of the white matter based on different measurements are commonly used to make inferences about connectivity and tissue properties, but there was no extensive study of the fits of these models to the data, and no assessment of the effects of measurement parameters on the model fits. In the study described here, we used cross-validation to evaluate two commonly-used models in a variety of measurement conditions. The work was published in [PLoS One](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0123272)

The project started with the collection of MRI data. Six participants were scanned in different experimental conditions. The data were collected in the Stanford Center for Neurobiological Imaging (CNI). The CNI has developed the Neurobiological Image Management System [Wandell et al. 2015], which captures the data from the scanner, archives it, and exposes a web interface that allows researchers to control access to the data, and copy it into the lab's data storage, a RAID system.

The data were preprocessed using standard procedures (in the sense that any practitioner of MRI would perform these steps on his or her data). This includes correction of motion artifacts, alignment to a common coordinate frame, and tissue type segmentation. These steps were performed once, at the beginning of the study. The code that performs these steps is part of the lab code distribution, [`vistasoft`](https://github.com/vistalab/vistasoft), freely available through Github. Preprocessing also relied on freely available software from other labs. 

The preprocessed data are publicly available through the Stanford Libraries SDR, as two [different](http://purl.stanford.edu/ng782rw8378) [collections](http://purl.stanford.edu/rt034xr8593). Most of the data was licensed under the Creative Commons Atttribution license, and a small subset was also released under the Public Domain Dedication License, for unencumbered use in methods development. 

Subsequent analysis was conducted on these preprocessed data, using a python library: [`osmosis`](https://github.com/vistalab/osmosis). This includes implementations of methods for fitting the data, statistical analysis, simulations and visualization, as well as utility functions  to handle parallel execution on an HPC cluster. The library depends on many components of the scipy stack, including `numpy`, `scipy`, `matplotlib`, `scikit-learn`. In addition, the code depends on components of the [neuroimaging in Python s libraries](https://nipy.org). Approximately 30% of the module code was covered by unit tests, with a particular emphasis on core modules and utility functions that were reused. A few end-to-end tests were implemented to track regressions. Development of the software was openly done on Github, and it was also released under an attribution license.

Scripts using the module code were developed using the IPython notebook. These scripts were run and edited many times, and as the project evolved a few of these were copied into a [documentation folder](https://github.com/vistalab/osmosis/tree/master/doc/paper_figures), with notebooks named "Figure1.ipynb", "Figure2.ipynb", etc, each corresponding to a figure in the paper. In writing of the paper, these figures were saved and additionally manually edited by hand to add labels and annotation, and then integrated into a Word file, which was used to collaborate on writing with the other authors. The writing process was not versioned throughout, but several versions of the article were submitted to the arXiv preprint server, while the article underwent peer review.

Most of the computations during the development of the project were conducted on a lab compute server, running an IPython notebook server. Thus, much of the development of the code was done on a laptop, over a web browser, connected to the server. However, some procedures described in the paper would require an inordinate amount of time, without the access that we had to an HPC cluster. For example, testing different settings of the regularization parameters required fitting the models hundreds of times. Data was accesible to the cluster through a mount of the lab RAID. Tasks run on the cluster were managed through a queue system (Sun Grid Engine), and a module was developed (`osmosis.parallel`) to facilitate submission of code to the cluster. These scripts could not be used as `ipynb` files, and were separately invoked on the command line, but they are included as part of the code distribution, recording these steps. 

Notebooks for steps that required parallel execution include both a 'cached' version (where parameters of the analysis are read from cached files), and 'complete' versions, which include the code that would have to be run to reproduce these results on a single machine. Parameter files were not made publicly available, and would have to be recomputed to reproduce.

Though reproduction of the results in the paper is relatively straight-forward, the library is not neccesarily useful as a tool for others to work with. During the work on this project, I became involved in an open-source project, which develops software for the analysis of dMRI data in python: [Dipy](http://dipy.org). Eventually, as the project matured, some of the ideas in `osmosis` were ported into Dipy. Mostly, these were reimplementations of software that was implemented in `osmosis`, with the necessary adjustments of the API, when this was incompatible. This is because some of the APIs did not match, and a better understanding of some of the underlying issues. 
`

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

A. Rokem, J. Yeatman, F. Pestilli, K.N. Kay, A. Mezer, S. van der Walt, B.A. Wandell (2015). Evaluating the accuracy of diffusion MRI models in white matter. PLoS One, DOI: 10.1371/journal.pone.0123272.

Ed H. B. M. Gronenschild , Petra Habets, Heidi I. L. Jacobs, Ron Mengelers, Nico Rozendaal, Jim van Os, Machteld Marcelis (2012). The Effects of FreeSurfer Version, Workstation Type, and Macintosh Operating System Version on Anatomical Volume and Cortical Thickness Measurements. PLoS One, DOI: 1371/journal.pone.0038234