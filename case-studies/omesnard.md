##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

We are members of a computational research group led by Prof. [Lorena Barba](http://lorenabarba.com) at the George Washington University in the department of Mechanical and Aerospace Engineering. 
One of our research projects focuses on studying animal flight by means of unsteady simulations at low/moderate Reynolds numbers, using immersed-boundary methods.
The work we describe in this case study was executed by the first author, PhD student Olivier Mesnard, but it fits in a broader program of research involving other group members.
We do our best to accomplish reproducible research and have for years worked to improve our practices to achieve this goal.
According to the "Reproducibility PI Manifesto," pledged by Barba in 2012, all research code written in the group is under version control and open source, our data is open, and we publish open pre-prints of all our publications.
For the main results in a paper, we prepare file bundles with input and output data, plotting scripts and figure, and deposit them in the [figshare](https://figshare.com/authors/Lorena_A_Barba/97553) repository.
These conditions all apply to our previously published work in Krishnan et al. (2014), studying the aerodynamics of flying snakes.
This case study describes what happened when we tried to reproduce our previous results, using different computational fluid dynamics (CFD) codes, including our own.


2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

How we understand the term "reproducibility" may be particular to our research area and others may understand it differently. We view it in the following way.
Given a set of inputs and a set of instructions, if two independent researchers can arrive at the same conclusions, the study deserves the tag "reproducible." 
It thus is distinguished from *replicability*, and may also involve the idea of tolerance (Drummond, 2009). 
In computational fluid dynamics, replication of a study can be achieved by using the same numerical code to re-generate the results, while reproducibility of the findings can involve using a different code (or even a different method). 
We learned from our experiences that reproducibility can be more challenging than replicability.

##### Workflow diagram

The core of your case study is a diagrammatic workflow sketch, which depicts your the entire pipeline of your workflow. Think of this like a circuit diagram: boxes represent steps, tools, or other disjoint components, and arrows show how outputs of particular steps feed as inputs to others. This diagram will be complemented by a textual narrative.

We recommend the site draw.io for creating this diagram, or you are also welcome to sketch this by hand. While creating your diagram, be sure to consider:

* specialized tools and where they enter your workflow
* the "state" of the data at each stage
* collaborators
* version control repos
* products produced at various stages (graphics, summaries, etc)
* databases
* whitepapers
* customers

Each of the two example case studies include a workflow diagram you can also use for guidance.

Please save your diagram alongside this completed case study template.

![workflow_diagram](omesnard.png)

##### Workflow narrative

Referring to your diagram, describe your workflow for this specific project, from soup to nuts. Imagine walking a friend or a colleague through the basic steps, paying particular attention to links between steps. Don't forget to include "messy parts", loops, aborted efforts, and failures.

It may be helpful to consider the following questions, where interesting, applicable, and non-obvious from context. For each part of your workflow:

* **Frequency:** How often does the step happen and how long does it take?
* **Who:** Which members of your team participate (or not)?
* **Manual/Automated:** Is the step automated or does it involve human intervention (if so, is it recorded)?
* **Tools:** Which software or online tools are used in the step? How are they used?

In addition to detailing the steps of the workflow, you may wish to consider the following questions about the workflow as a whole:

* **Data:** Is your raw data online?
   * Is it citeable?
   * Does the license allow external researchers to publish a replication/confirmation of your published work?
* **Software:** Is the software online?
   * Is there documentation?
   * Are there tests?
   * Are there example input files alongside the code?
* **Processing:** Is your data processing workflow online?
   * Are the scripts documented?
   * Would an external researcher know what order to run them in?
   * Would they know what parameters to use?

*(500-800 words)*

Our research lab developed over the years a consistent workflow to do reproducible research. Our previous published study (Krishnan et al., 2014) already followed the PI Manifesto (Barba, 2012). We used an immersed-boundary projection method to compute the  flow around a flying-snake cross-section (a lifting bluff body) at moderate Reynolds numbers. The method requires to solve a modified Poisson system with an iterative algorithm provided by a external linear algebra library. The numerical code [cuIBM](https://github.com/barbagroup/cuIBM) is hosted on the version-control platform GitHub, the manuscript was first available on arXiv, and replicability instructions have been uploaded to figshare. We did our best to make that study replicable by others. Below, we describe the workflow we used attempting to reproduce, with various software, a highly unsteady flow dominated by vorticity.

We used a total of four computational fluid dynamics software to replicate and reproduce the study:
- [cuIBM](https://github.com/barbagroup/cuIBM), the GPU open-source code previously used,
- [PetIBM](https://github.com/barbagroup/PetIBM), a multi-CPU version of cuIBM,
- [IBAMR](https://github.com/ibamr/ibamr), an immersed-boundary method code that implements a different mathematical formulation,
- IcoFOAM, the incompressible laminar solver of [OpenFOAM](http://www.openfoam.org/).

We started with IcoFOAM to look at the possibility of capturing the lift characteristics of the geometry studied in our previous work (Krishnan et al., 2014) using a more traditional approach: a body-conforming mesh. We chose IcoFOAM as it is open-source and documented -- both code- and users-documented -- and has an extended users-community. We wanted to use similar inputs than Krishnan et al. (2014), as much as possible, to reproduce their results. The mesh quality as well as proper boundary conditions were essential in capturing the flow features.

We moved on IBAMR, an open-source software hosted on GitHub, mainly developed by [Boyce Griffith](http://www.cims.nyu.edu/~griffith/), to investigate the possibility to derive the same conclusions than Krishnan et al. (2014) with a different immersed-boundary formulation. Bhalla et al. (2013) published a detailed validation of the method implemented in the software and various examples can be found on the code repository.

cuIBM and PetIBM are both being developed our research lab and implement the same immersed-boundary method. As a matter of reproducibility, we intend to do our best to provide code-documentation (Doxygen), users documentation (GitHub wiki), as well as basic examples/tutorials. In cuIBM, we use [CUSP](https://github.com/cusplibrary/cusplibrary), an open-source library for sparse linear algebra on CUDA architecture GPUs. We used cuIBM to confirm the replicability of our previous findings (Krishnan et al., 2014). It is important to note that we had to use the same version of the code with the same version of the algebra library to obtain the same numbers.
In PetIBM, we implemented the same immersed-boundary method using this time the [PETSc](http://www.mcs.anl.gov/petsc/) library. We observed that using a different linear algebra library changed the conclusions about the snake aerodynamics.

We chose Python to automate pre- and post-processing steps -- the different scripts are version-controlled and code-documented and allow command-line arguments (to avoid as much as possible code-modification from users).  We also took advantage of the Python interpreter included in the visualization tools [Paraview](http://www.paraview.org/) and [VisIt](https://wci.llnl.gov/simulation/computer-codes/visit/) to automate the post-processing part of OpenFOAM and IBAMR simulations. In addition to that, we used Jupyter Notebooks and Markdown files to present project advances during various meetings -- our group-meetings are version-controlled on GitHub.

Finally, once the results have been gathered and analyzed, the manuscript is written using LateX and version-controlled in its own GitHub repository to facilitate communication between collaborators. To advocate open-science, the manuscript will be available on arXiv and for each simulation and each figure reported in the manuscript, we will provide a reproducibility package as a warranty of the veracity of our results. This package includes the version of the software (as well as the one of each dependency), the input parameters (for both the simulation and the post-processing), information related to machine architecture, and the necessary scripts to run and post-process the simulation.

*References*:
- Bhalla, A. P. S., Bale, R., Griffith, B. E., & Patankar, N. A. (2013). A unified mathematical framework and an adaptive numerical method for fluid–structure interaction with rigid, deforming, and elastic bodies. Journal of Computational Physics, 250, 446-476.
- Drummond, C. (2009). Replicability is not reproducibility: nor is it good science.
- Krishnan, A., Socha, J. J., Vlachos, P. P., & Barba, L. A. (2014). Lift and wakes of flying snakes. Physics of Fluids (1994-present), 26(3), 031901.

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

Throughout the project we faced several difficulties in reproducing the highly unsteady flow around the flying-snake cross-section. With IcoFOAM (body-conforming approach), the quality of the mesh as well as the use of non-reflecting boundary conditions were the keys to confirm previous findings about the snake aerodynamics. Although we were able to replicate the results using the same cuIBM version with the same version of the external library, our reproducibility attempt, with PetIBM, failed with a different linear algebra library. Finally, IBAMR was capable to reproduce the snake feature only after modification of the body mesh-discretization.
For this study, we needed to compute about 80 time-units of flow simulation. The duration of the simulations varies between one and three days on a super-computer and the numerical solution weights between 3.5 and 16G. Keeping a clean, up-to-date, and detailed lab notebook appeared to be vital to track all simulations.
Most of the simulations were run on a HPC cluster at the George Washington University. As we moved data back and forth between different machines (to run the simulation or to store the solution on an external device), a lab notebook made it easier to remember the location of each simulation. 
Getting used to new computational fluid dynamics software was also time-consuming.  It took longer to familiarize with code with poor users-documentation.
Finally, we also spent some time to develop automated scripts to analyze the numerical solution from different software (with different output format).

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

##### Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*

We use the version-controlled platform GitHub to achieve a reproducible workflow. GitHub facilitates collaboration when developing numerical codes. The platform allows to create wiki pages for users-documentation. We also use GitHub to write manuscripts, to record our group-meetings, and to store teaching materials.

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

Reproducibility is a chance to prove that you can be trusted as a scientific researcher. Ensuring that a manuscript (along with the data used to generate the figures) is reproducible makes it easier for others to corroborate (but reject) your research hypothesis. We believe that reproducible research would prevent scientists to reinvent the wheel.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

Our advisor , Prof. Lorena Barba, plays a major role in raising awareness about reproducible research. Back in 2012, she posted a "Reproducibility PI Manifesto" back in 2012 that we use along the studies.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

Reproducible research can be time-consuming; it requires rigorous methods and organization. At various moments during the project, we had to pause and ask ourself if our research was currently reproducible.

4) What do you view as the major incentives for doing reproducible research?

Making your research reproducible -- providing reproducibility packages along with the manuscript -- is a way to showcase your skills, an excellent communications medium to convey ideas, and a fast way to get feedbacks on your work. If the research community  is inclined to put more effort in doing reproducible work, it would prevent scientists from re-inventing the wheel.

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

* Drummond, C. (2009). Replicability is not reproducibility: nor is it good science.
* "Reproducibility PI Manifesto", L. A. Barba. (13 December 2012). 10.6084/m9.figshare.104539
Presentation for a talk given at the ICERM workshop "Reproducibility in Computational and Experimental Mathematics". Published on figshare under CC-BY.
* [Software Carpentry](http://software-carpentry.org)
* Software Testing -- Udacity MOOC (https://www.udacity.com/).
* P.B. Stark (2015). Science is "show me", not "trust me". [Blog post](http://www.bitss.org/2015/12/31/science-is-show-me-not-trust-me)

