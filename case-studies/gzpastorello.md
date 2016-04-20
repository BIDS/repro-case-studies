##### Title

Generation of uniform data products for AmeriFlux and FLUXNET

##### Introduction

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

I'm [Gilberto Pastorello](http://www.gilbertozp.org/), a [Research Scientist](http://crd.lbl.gov/departments/data-science-and-technology/idf/staff/gilberto-pastorello/) at Lawrence Berkeley National Laboratory, doing research on life-cycle management of scientific data, encompassing data and metadata structures and linkages, data quality and data uncertainty quantification, and end-to-end data systems. The part of my work described here involves development of data processing pipelines and data management solutions within the environmental domain. This work is done for the [AmeriFlux](http://ameriflux.lbl.gov/) and [FLUXNET](http://fluxnet.fluxdata.org/) research networks.


2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

For this case study, reproducibility means being able to apply standard methods to process heterogeneous data sets to generate comparable data products. The data sources for our processing are distributed across very different ecosystems, with data acquired, processed, and quality checked by different teams. The data products we generate from these data sets need to be in the same scales and have comparable levels of quality, representativity, etc.



##### Workflow diagram

[Diagram](gzpastorello.pdf)



##### Workflow narrative

Multiple Science Teams collect carbon, water, and energy fluxes from over 800 field sites across the world. Currently, more than 400 of these sites share their data with regional networks such as [AmeriFlux](http://ameriflux.lbl.gov/), allowing the creation of data products with a global scope for the [FLUXNET](http://fluxnet.fluxdata.org/) network. These sites are operated independently and methods for data collection, processing, and data quality control by the Science Teams can vary significantly. Our workflow aims at processing these heterogeneous data sets to generate data products that are comparable across these sites. A general view of the steps in our workflow is shown in the figure. In this context, reproducibility is strongly related to identifying and documenting data quality control checks, parameterizations for processing, sequences of correction steps, and data filtering.

The pipeline is executed every time new data are sent to us by the Science Teams. We keep track of multiple submissions with a combination of simple incremental counters for versions and timestamps -- logs of data transfers are stored in a relational database. The frequency of data submissions can range from daily to yearly updates from a Science Team. All executions of the pipeline generate a version, with successful executions being made public after being vetted by the Science Teams.

The first few steps are related to data quality and aim at identifying serious quality issues and making data quality more uniform across sites. Specialized algorithms and visualization methods are used in these steps. Automated generation of flags and manual inspection of data sets are done first, followed by the compilation of metrics about the data and checks. Any decision to change the data sets is first shared with the Science Team and confirmed before being executed. Major issues are identified and solutions are developed in collaboration with Science Teams. A custom issue tracking system developed by us is used to keep track of interactions with Science Teams and the issues being addressed in the data sets. The information in this issue tracking system is private and accessible only to our team and the Science Team for the field site providing the data, but reports and status information from this system can be made available with a published data product. Changes to data are also documented in log files and quality flags that are added to the data sets themselves, these being made available along with data products.  Changes and corrections generate a new version of the input data and the pipeline starts again from this new version.

The central portion of the workflow includes the processing steps for heat, carbon and micrometeorological variables. The parameters used to configure these executions are stored with the data sets, and specialized checks are also executed within each step. The results from most of these checks are stored as quality flags added to the data sets. Versions of the code used for these steps are also recorded in the data set's metadata.

The product merging step reformats the data into common structures and combines quality information into quality flags at a higher level of abstraction, to simplify using the data sets. The uncertainty quantification step generates quantiles representing uncertainty intervals originating from each of the processing steps, also becoming part of the data products.

The product evaluation step involves looking at the resulting data products in the context of the field site by interpreting the results for physical feasibility and biological and ecological significance. Checks against larger scale climate data are also performed. The information compiled in this step is shared with Science Teams for their evaluation and, if approved, shared publicly.

Data as shared by the Science Teams are made available online as well as the data products generated by our own processing. The code used for quality checks and product generation is going through an overhaul, with documentation and tests being added, and should be made available as a product in the future. Currently, the code is executed in a few institutions that can run the processing, with a shared private code repository holding the code.



##### Pain points

The execution of this pipeline can happen several times before acceptable results are reached, and it also includes several interactions with the Science Teams resulting in changes to the input data sets. The changes can be applied by the Science Teams or by our team. With multiple iterations, the changes that are needed to make a data set correct can be spread across many versions of the input data. Consolidating these changes is particularly difficult, especially when the changes were applied to versions that led to unsuccessful runs, which could be inadvertently ignored.

Keeping versions consistent across multiple processing instances can be a challenge. We use mapping of versions of inputs to outputs, but with outputs influencing what a new version of the inputs look like, these mappings are not always straightforward.

Many of the data sets we handle span decades of data collection, processing, and curation by multiple people. Since the teams are widely distributed and follow potentially different data collection and processing protocols, fully automated reproducibility is difficult to be achieved. A workaround has been to document the choices in collection and processing data in such cases.

Combining reproducibility issues with credit issues for data sets is another challenge. Giving proper credit to data providers and data processors/curators is an essential part in large data sharing efforts. Data sharing policies help with assigning proper credit. However when multiple versions of the data sets are being shared -- often spanning decades -- this also requires keeping track of many different types of contributions to each data set.



##### Key benefits

Without the use of versioning and issue tracking, for instance, it would be unfeasible to fully document choices for the data sets that affect aspects such as data quality or data processing parameters.



##### Key tools

Data and software versioning are certainly the main practices adopted in this case study. We are currently assigning versions to data and software in a coordinated way, to allow assessment of changes to data and code. We use a private Subversion server for code version control. We developed a custom Web-based system called FIT (Flux Issue Tracking) for tracking the interactions with Science Teams and data quality issues for data sets. FIT was also adapted to be used for tracking code related issues.



##### General questions about reproducibility

1) Why do you think that reproducibility in your domain is important?

The data sets in this case study offer unique insight into ecosystem-scale behaviors for biological systems. These data can be used, for instance, in the validation and assessment of climate models at much larger scales (regional, continental, and global). For this type of application, being able to recreate data products uniformly is essential for the credibility of these validations/assessments.


2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

Many of the practices were strongly motivated by requirements from the domain itself. Specific solutions were adapted and implemented following literature on handling these requirements -- e.g., versions, documentation for software parameterization, and others.


3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

Since a lot of the pipeline involves identifying data quality issues that can originate from many different sources, we have to be precise when making documentation on these issues available. Only issues applicable to a specific version of a data set should be associated with it and coordination with Science Teams is essential to properly create this documentation. Also, the quality checks aim at improving quality and making data products more uniform, and not changing the workflow already adopted by data contributors.


4) What do you view as the major incentives for doing reproducible research?

Research involving large and/or distributed teams is much easier when allowing effective reproducibility. When multiple team members understand and can generate products, it is much more likely that problems will be identified early, questions from external members of the community will be answered more easily, and funding agencies will have documented product releases (data and software), which can be combined with other types of publications in assessments of scientific impact.


5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

While version control is widely adopted for software code, this is not necessarily the case for data. Consistently keeping track of versions of a data set at a minimum helps with data changes and is well worth the extra effort. Another lesson we learned early was that issue/bug tracking ideas and tools can simplify data management activities, and can also be valuable in building the history of a data set and generating its documentation.


6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

While not always featuring fully developed practices or tools, reproducibility scientific events (and their published proceedings) often showcase new and interesting ideas. Examples are the International Provenance and Annotation Workshop (IPAW) and the Workshop on the Theory and Practice of Provenance (TaPP).
