##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Jan Gukelberger, I am a computational condensed-matter physicist, who recently completed his PhD at the Institute for Theoretical Physics, ETH Zurich. This case study describes a project I worked on during my first year as a PhD student (2010-2011).


2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In general, given a publication (in a refereed journal), source codes and raw data (which might be available publicly or in the institute's repositories), an expert from my field should be able to understand, and in principle repeat, every step of the study from the running of the correct version of the simulation code to the final results presented in the published paper.

##### Workflow diagram

[Diagram](jgukelberger.pdf)

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


Since the simulations may require a large amount of compute resources (on clusters or large workstations), it is usually not feasible or desirable to re-run the whole process in one go. We therefore usually adapt a two-step approach: The output of the simulation runs is treated as primary/raw data, which is archived along with log files containing detailed information about source code version, execution environment, and input parameters. The evaluation and transformation of this raw data to the final results (typically figures with plots) should then be as easily repeatable as possible, ideally with a single push of a button or script execution.

In this study, we opted to publish the raw data as supplementary information on the publisher's (APS) web server and provide workflow files for the VisTrails system, which would retrieve the raw data from this server and recreate the figures contained in the paper. This way, any reader can inspect in detail all steps of our data analysis.

The study is published as Phys. Rev. B 85, 045414 (2012), DOI:10.1103/PhysRevB.85.045414 .


##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

During the project, the main pain points were connected to the facts that the data evaluation had to be done in the VisTrails GUI and the opaque-ish VisTrails workflow file format:

   * Data evaluation (execution of VT workflows) could not be scripted at that time.
   * The evaluation could not be run on a cluster/via ssh.
   * Version management was harder because viewing differences between versions was not as easy as looking at the diff file for a Python script.
   * This also made the synchronization of workflows between different machines (e.g. laptop and workstation) less straightforward.

A separate painful process was, once the study was completed, working with the publisher to create a working "reproducible paper" on their servers. Here, the main problem was the need for cross-references between the manuscript, the VT workflows, and the raw data, because the final location of each component only becomes available in the last step of the production process, when the files cannot be changed anymore without manual intervention from the production team. Some aspects of this issue were explained in detail in our report https://www.usenix.org/event/tapp11/tech/final_files/Bauer.pdf .

When now inspecting the "reproducible publication" on the APS server, three years after publication, some mid- to long-term issues become obvious, because both the used software and the publisher's infrastructure is evolving:
   
   * The instructions we provided in the supplementary materials section accompanying the article do not work with the current VisTrails version: In the most recent stable VisTrails release (2.2), the alps package seems to be broken and needs to be patched with the latest (not-yet-realeased) ALPS version. Otherwise initialization of the ALPS package fails and the workflow cannot be executed.
   * The APS journals were not able to guarantee a long-term stable location for supplementary material. In fact, the URL has already changed, such that the workflows fail to fetch the raw data from the APS server, unless the URL is fixed manually in each workflow. For one specific example, the original location http://prb.aps.org/epaps/PRB/v85/i4/e045414/dyl_ladder_gap.zip has been changed to http://journals.aps.org/prb/supplemental/10.1103/PhysRevB.85.045414/dyl_ladder_gap.zip .
     Also, the cause of the error is not easy to fix for the uninitiated, because the DownloadFile module actually succeeds (it downloads the html file shown at the old URL), but the subsequent UnzipDirectory module fails with the message "BadZipFile: File is not a zip file".

For these reasons I would now prefer to publish a self-contained archive containing the raw data and a  script in a wide-spread language, such as Python, which re-runs the analysis and re-produces the figures. This would be more robust with respect to changes in the publisher's infrastructure. Also, backwards compatibility issues can be expected to be solvable more easily in the long run for scripts in a wide-spread language, compared to special purpose solutions like VisTrails (no matter how professional and helpful the developers of the latter may be at the moment).


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
