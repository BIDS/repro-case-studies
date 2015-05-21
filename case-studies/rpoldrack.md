##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Russell Poldrack, and I am a professor in the Department of Psychology at Stanford University.  My work uses neuroimaging, genomics, and behavioral studies to examine the brain systems involved in decision making and executive control.  Many of our workflows use high-performance computing due to the large data and complex nature of the workflows.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In the context of my case study, "reproducibility" means the ability to exactly reproduce the analysis workflow that was used to obtain the results reported in a manuscript. More generally, I take the term to also emcompass the consistency of results across different workflows or datasets. 

##### Workflow diagram


##### Workflow narrative

Referring to your diagram, describe your workflow for this specific project, from soup to nuts. Imagine walking a friend or a colleague through the basic steps, paying particular attention to links between steps. Don't forget to include "messy parts", loops, aborted efforts, and failures.

This workflow is meant to outline the analysis of a complex dataset including neuroimaging, behavioral, genomic, and metabolomic data (http://www.myconnectome.org).  


It may be helpful to consider the following questions, where interesting, applicable, and non-obvious from context. For each part of your workflow:

* **Frequency:** How often does the step happen and how long does it take?
* **Who:** Which members of your team participate (or not)?
* **Manual/Automated:** Is the step automated or does it involve human intervention (if so, is it recorded)?
* **Tools:** Which software or online tools are used in the step? How are they used?

In addition to detailing the steps of the workflow, you may wish to consider the following questions about the workflow as a whole:

* **Data:** Is your raw data online?
- yes - it is currently available via S3, and will ultimately be made available through the openfmri.org project. The python package also includes a function to download various aspects of the raw data.

   * Is it citeable?
It will be citeable using an OpenfMRI URI (http://openfmri.org/ds000031)

   * Does the license allow external researchers to publish a replication/confirmation of your published work?
The data are released under a public domain dedication, so that anyone can do anything they wish with them.

* **Software:** Is the software online?
Yes, the software is available via a github repository.

   * Is there documentation?
There is currently minimal documentation.

   * Are there tests?
Currently the only test is one that compares the results of the full workflow to a set of results cached on S3.

   * Are there example input files alongside the code?
N/A - the actual input files are automatically downloaded by the workflow.

* **Processing:** Is your data processing workflow online?
   * Are the scripts documented?
   * Would an external researcher know what order to run them in?
   * Would they know what parameters to use?

*(500-800 words)*

##### Pain points
- Extra work generalizing the code to work on an arbitrary system
- Concern about exposure of errors or poor coding.
- What is the right technology for sharing a reproducible workflow?
- What is the level of user at whom we are targeting this?

*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

##### Key benefits
- Provides a degree of detail that could not be feasibly included in the publication.
- Increases the degree of trust amongst others in the field in one's results
- Provides an example for others in our subfield of how to implement reproducible shared workflows.

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
