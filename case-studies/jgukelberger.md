##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Jan Gukelberger, I am a computational condensed-matter physicist, who recently completed his PhD at the Institute for Theoretical Physics, ETH Zurich. This case study describes a project I worked on during my first year as a PhD student (2010-2011).


2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

I consider a study to be reproducible if, for all results in the final publication

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

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

During the project, the main pain points were connected to the facts that the data evaluation had to be done in the VisTrails GUI and the opaque-ish VisTrails workflow file format:

   * Data evaluation (execution of VT workflows) could not be scripted at that time.
   * The evaluation could not be run on a cluster/via ssh.
   * Version management was harder because viewing differences between versions was not as easy as looking at the diff file for a Python script.
   * This also made the synchronization of workflows between different machines (e.g. laptop and workstation) less straightforward.

When now inspecting the "reproducible publication" on the APS server, three years after publication, some mid- to long-term issues become obvious, because both the used software and the publisher's infrastructure is evolving:
   
   * The instructions we provided in the supplementary materials section accompanying the article do not work with the current VisTrails version: In the most recent stable VisTrails release 2.2, the alps package seems to be broken and needs to be patched with the latest (not-yet-realeased) ALPS version. Otherwise initialization of the ALPS package fails and the workflow cannot be executed.
   * The APS journals were not able to guarantee a long-term stable location for supplementary material. In fact, the URL has already changed, such that the workflows fail to fetch the raw data from the APS server, unless the URL is fixed manually in each workflow. For one specific example, the original location http://prb.aps.org/epaps/PRB/v85/i4/e045414/dyl_ladder_gap.zip has been changed to http://journals.aps.org/prb/supplemental/10.1103/PhysRevB.85.045414/dyl_ladder_gap.zip .
     Also, the cause of the error is not easy to fix for the uninitiated, because the DownloadFile module actually succeeds (it downloads the html file shown at the old URL), but the subsequent UnzipDirectory module fails with the message "BadZipFile: File is not a zip file".
	


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
