##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Anthony Arendt and I hold a joint appointment as a Senior Research Scientist at the Applied Physics Laboratory, and a Research Fellow at the eScience Institute, University of Washington. I am part of a research team that studies the impact of glaciers on rising global sea levels, with a focus on the glaciers of Alaska and northwestern Canada. During the past 20 years my colleagues at the University of Alaska Fairbanks have been measuring the elevation changes of Alaska's glaciers using LiDAR data collected from a small aircraft. We use these data to estimate total changes in mass of each observed glacier, and then extrapolate these data to unmeasured glaciers based on information acquired from satellite imagery. From this we produce detailed maps of the spatial distribution of glacier mass change and the total contribution of these ice masses to global ocean change.

During the 20 year duration of the project the data analysis has evolved from manual manipulation of flat files, to a semi-automated workflow that integrates GIS, relational database and Python tools within a cloud computing framework. Here we describe the workflow which culminated in a recent publication (Larsen et al., 2015). Core developers of the software include Evan Burgess, Christian Kienholz, Justin Rich, Anthony Arendt and Christopher Larsen. 

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

Reproducability is a crucial component of our workflow due to the dynamic nature of our monitoring campaign, and the need to constantly update the position and elevation of glaciers as they change in response to climate. We achieve reproducability through maintaining consistency in the input datasets; utilizing a series of scripts to automate data ingest and filtering; storing raw and filtered/processed data in a relational database; generating data objects that handle typical data analysis functions; and scripting all manuscript figures in Jupyter notebooks.  

##### Workflow diagram
 
The majority of our workflow is hosted on a single Microsoft Azure Linux Virtual Machine. Only two components exist outside of this cloud-based framework and are comprised of 

Each year a new set of airborne data are collected, comprising of LiDAR point cloud data and GPS observations of the precise aircraft position. These millions of points are condensed into gridded tiles and the filtered for outliers. The data are extrapolated to the surveyed glacier to obtain an estimate of the total volume change relative to an airborne measurement from an earlier date. This produces a single text file per glacier per elevation differencing. The data are stored on a server in Fairbanks, ordered into folders by glacier name.

In a 


For our recent manuscript we ingested approximately 150 of these text files. Each file is 

We recommend the site draw.io for creating this diagram, or you are also welcome to sketch this by hand. While creating your diagram, be sure to consider:

* specialized tools and where they enter your workflow
* the "state" of the data at each stage
* collaborators
* version control repos
* products produced at various stages (graphics, summaries, etc)
* databases
* whitepapers
* customers

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
