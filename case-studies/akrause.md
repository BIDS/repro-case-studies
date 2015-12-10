##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

Andy Krause, Lecturer in Property (Real Estate) at the University of Melbourne.  Andy's research focuses on the spatial analysis of real estate markets, particularly in regards to valuation and location. 

Hossein Estiri, Senior Fellow in the Institute of Translational Health Sciences at the University of Washington. Hossein uses data science approaches to study urban energy and health.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

"Reproducibility" means that a subsequent interested party can openly access the data, code, analytical workflow and data provenence to re-create the research (and ideally produce identical results) WITHOUT consulting the original researcher(s). In this context, "reproducibility" can facilitate the verification of results from a given research project and also accelerate new research discoveries by providing reproducible modules that can be applied in other settings and/or for other purposes.

##### Workflow diagram

[Diagram](aKrause.pdf)

##### Workflow narrative

This research analyzes the household location choices of American households in the largest 50 metropolitan areas in the United States.  Households are broken down by five-year age cohorts (based on the age of the head of the householder) and mapped against the household's distance (census block group level) from the central business district of the metropolitan area in which they reside.  In polycentric regions such as Seattle (Tacoma, Bellevue and Everett as alternative CBDs), analyses are conducted on distance to core center as well as secondary centers. An initial paper reporting the results is currently under review.

All data, code and analytical workflow are hosted on-line.  Code and analytical workflow, including analytical script and custom function sets, are written in R and found on the project's [Github Repository](http:/github.com/andykrause/hhLocation).  The complete set of raw data is available through the U.S. Census (discussed below).  Users wishing to skip the data compiling and/or cleaning steps can download the compiled or cleaned data from the project's [Dataverse Repository](http://dx.doi.org/10.7910/DVN/QDEMVF).  

The *hhLocAnalysis.R* file in the main analysis script and the only file that needs to be executed.  Two key process parameters must be manually set:

1. **reBuildData** - do you want to go through the entire data compilation process?
2. **reCleanData** - do you want to re-clean data?

A third parameter -- the location of a suitable data directory -- must be set if **reBuildData** is set to TRUE. 

The user must also specify the directory where the [Code Repository](http:/github.com/andykrause/hhLocation) was cloned (**codeDir**). Additional parameters regarding the location of the downloaded intermediate data (see below) -- **rawDataFile** and **cleanDataFile** -- and a path to output the figues to (**figurePath**) must also be set. This is the extent of manual operations. All other processes run automatically.  If the data is fully built from scratch this process may take multiple hours. Additionally, the user may change a number of the optional paramters that handle the distance scaling, overall number of metro-regions to analyze, maximum distance from CBD center to include in the data and whether or not computational progress is reported. 

The raw data for this study comes primarily from the U.S. Census's FTP site.  Data files for every county in the fifty largest metropolitan areas are downloaded, unzipped, cleaned and written out as a standardized .csv file.  Custom functions to handle the data acquisition process were written in R and are found in the *buildHHData.R* and *buildCBSAData.R* files in the repository.  This time consuming (and data storage intensive) process of compilation can be avoided by setting **reBuildData** to FALSE. If either **reBuildData** or **reCleanData** are set to FALSE then the intermediate data sets (raw compiled and/or cleaned) must be downloaded from the [Dataverse Repository](http://dx.doi.org/10.7910/DVN/QDEMVF).  Two additional files containing city and CBSA (metro region) names are also needed for the analysis.  These files are available in .csv form in the code repository. 

After the cleaned data has been compiled and built (or downloaded from Dataverse), the main analysis script then calculates the location quotient distance profiles and plots a variety of different visualizations of the results. Final results, both tabular and visual, are then combined in an RStudio/Knitr file along with the narrative to create the final document (compiled in LaTeX).  The full data provenance is described and hosted on the code repository via a Markdown file.  Also note that the collaborative website [Authorea](https://www.authorea.com/users/18208) (which offers git-based tracking and LaTeX support) was used by the authors to write the first draft of the narrative portion of the report.  

##### Pain points

There are two major steps that we consider particularly painful.  The first is convincing yourself (and co-authors) to take the time to properly document every action and to take the time to fully annotate the analytical workflow.  This can be especially difficult when deadlines arise or when co-authors do not see the value in reproducibility.  The second is the need to write custom functions that are generalizable.  Writing very specific, single use function can be easy, but are rarely useful in more than a single instance.  Good reproducible research contains flexible functions than can accomodate changes or permutations thereby allowing subsequent users to expand/change your original analysis.  

The current peer-review process also presents a considerable hurdle to reproducibility.  In order to remain anonymous in the review process, we've had to build a set of anonymous code and data repositories and interactive websites for the review process and then switch over to our own repos after the paper has been accepted. It means a lot of extra work as well as remembering which Github count we are signed into at all times.  Along this line, judging by usage statistics, reviewers have been uninterested in actually examining the hosted code, data or results. 

##### Key benefits

For us the biggest benefit is efficiency.  The first time we do an analysis it usually takes longer than colleagues, but each time after the time savings simply multiply.  One situation where this is particulary helpful is in responding to peer reviewer comments and requests.  Changes to assumptions or sensitiviy tests on parameters can be done in a matter of hours (or minutes), not days or weeks.  This greatly shortens the re-submittal response time.  Related, we constantly find ourselves borrowing old code and re-purposing it, making new analyses easier and faster.  

(Andy) Better organization is another benefit.  No more folders full of data files with version names and dates. No more mystery fields in a dataset. No more starting all over after forgetting what was previously done. My students and their Excel sheets with dozens of tabs and screen clips from SPSS remind me of this benefit every semester. I am slowly incorporating more and more reproducibility into my classes, with the intent of breaking some of these bad habits.

(Hossein) Another benefit would be for progress general research. Beyond the theoretical approach that can be used to study other metropolitan patterns, functions that we built in this research can be applied to facilitate other forms of research using census data. Researchers can adapt these functions to address other purposes. In an ideal scientific world where all research is reproducible, research will be more efficient because of the code that can be shared, re-used, or adapted for research or non-research purposes.

##### Key tools

The RStudio IDE and their related Shiny Apps (interactive web applications) have been a huge help in our reproducible research.  If you are an R programmer and want to share your visualizations with non-programmers, we highly recommend these tools from RStudio. 

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

(Andy) A majority of quantitative analysis in real estate (both academic and professional) is usually duplicated by numerous parties, widely disseminated and frequently updated; all characteristics that benefit from reproducible analyses. Despite these core facts of the discipline, there is very little, if any, discussion on or attempt to create reproducible research in the field. 

(Hossein) In general, the importance of reproducibility in policy-/decision-oriented fields is not clear. It can certainly improve policy research, but one could debate whether or not reproducibility has direct benefits for decision-making.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

(Andy) My pre-academic background was as part of a team of expert witnesses in litigation support.  In this industry, any analysis that was produced had to be reproducible by the opposition and therefore, my firm was constantly striving to produce more efficiency in their reproducible analyses.  

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

(Andy) Two challenges exists in the real estate field.  First, most data is proprietary and expensive and therefore it is hard to share data.  Second, it is a small field that is composed of many senior individuals (both in academia and industry), many of whom are very resistant to change. 

(Hossein) In health sciences the biggest concern is around data privacy. For example, research on individual-level patient information can hardly become fully reproducible, within conventional workflows.

4) What do you view as the major incentives for doing reproducible research?

Doing reproducible research is like installing solar panels in your home. It will cost you at the beginning, but down the road you will get benefits such as time savings, better quality output and the increased opportunity to collaborate/share ideas.  

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

No more manual data cleaning.  Use code.  

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

For collaboration, if you want to get away from LaTeX, you can try [Authorea](https://www.authorea.com/). However, this is not a long term solution.

If you are in Australia, the [University of Melbourne's Research Platforms](http://blogs.unimelb.edu.au/researchplatforms/) group offers a number of Research Bazaars, Software Carpentry and Reproducibility-related courses and event.  It is open to researchers world-wide.  
