### Dissecting computational methods used in a biogeographic study

K.A.S. Mislan  
Postdoctoral Associate  
eScience Institute  
School of Oceanography  
University of Washington

##### Introduction

I am an ecophysiologist and my research focuses on organism-environment interactions in the ocean.  In particular, I am interested in forecasting the effects of climate change on marine ecosystems.

Reproducibility means that sufficient descriptive information and resources are provided for someone to be able to repeat the same study. As part of my research as a scientist, I write code to manipulate and visualize large quantities of data to obtain results. I believe that my code should be adapted and made available so that it is usable by others in my field.

I recently published research on the fundamental niche of pelagic animals in the global ocean. The study included a comparison of blood-oxygen binding characteristics of different species obtained from published papers.  Thresholds for blood-oxygen binding characteristics were mapped in the ocean using gridded oceanographic data.  My workflow narrative details my process for obtaining and analyzing data for the project.  In order to increase the reproducibility of the study, code used for the project was put in a long-term archive.

**Research paper**:  
Mislan, K. A. S., Dunne, J. P. and Sarmiento, J. L. (2016), The fundamental niche of blood-oxygen binding in the pelagic ocean. Oikos. [https://doi.org/10.1111/oik.02650](https://doi.org/10.1111/oik.02650)

**Code Archive**:  
Mislan, K. A. S., Dunne, J. P. and Sarmiento, J. L. (2015). P50 Depth Analysis v1.0. Zenodo. [http://dx.doi.org/10.5281/zenodo.31951](http://dx.doi.org/10.5281/zenodo.31951)

##### Workflow diagram

![Research Workflow](kasmislan_workflow_v5.pdf)

##### Workflow narrative

Obtaining data from existing resources was the first step.  World Ocean Atlas 2009 (WOA09) data is publicly available through the National Oceanic and Atmospheric Administration (NOAA) National Centers for Environmental Information. The WOA09 data is on a geographic grid and available in several different file formats. I downloaded the network common data form (netCDF) file format.  NetCDF format facilitates access and sharing of scientific data in arrays. There are many tools available to read and manipulate netCDF files. NOAA Ferret is publicly available software for visualization and analysis and has built-in functions designed for efficient processing of geographic data in netCDF format. One of the objectives of the analysis was to vary two input parameters and determine the effect on geographic characteristics. I automated the process of creating ferret scripts with different input parameters by writing a shell script that generated and processed NOAA ferret scripts (.jnl files).  The processed files were saved as netCDF files.    

R and Python were used to create the figures although it would have been possible to create all the figures in one or the other of these software packages. I learned R before Python so I tend to do most of my analysis in R because I am most familiar with it.  However, I like the tools for making geographic plots in Python so I used Python to make the geographic plots.  

The physiological data was gleaned from published studies found through Google Scholar searches for key words. As the data was extracted from the papers, it was put into a spreadsheet. The data of interest was often available in tables and the text of the papers. In some cases, the data was only available in scatter plots.  The ruler tool in Adobe Photoshop was used to manually extract the data from plots. Once all the information from the studies was entered into the spreadsheet, the data from the spreadsheet was saved as a tab-delimited text file. The data was then read into R to determine parameters for the analysis of the oceanographic data.  Additionally, the data was plotted in a scatter plot in R and each point in the plot had a number assigned to it. Information about the individual points was put into two tables. However, it was inefficient to obtain the information by looking between the numbers on the plot and the two tables.  Therefore, I created a web-based interactive plot that includes the information from the tables using a javascript library called Data-Driven Documents (D3).  

I created figures and wrote the paper.  Code is not usually included in the methods section of the paper due to space and formatting constraints. However, the code tells a much more complete story of my analyses.  I adapted the code and provided documentation so that the code could be used by someone else in the same way that I used it in my study. Therefore, I changed as little of the code as possible when adapting it to be independent of my operating system.

In order to prepare my code for archiving, I made some modifications to the code.  I created a folder structure that would make it easy for a user to find files. The folder structure included a folder for code and folders for input files to run the code and output files produced by the code. I annotated my code while I was writing it, but the annotations were usually short and meaningful only to me. Descriptive annotations were added to the code being archived. I also changed the file paths to be referenced solely within the folder structure (../../) so that the code is independent of my home directories (/Users/kasmislan/code/project).  

My code works on my computer, but it might not work the same way on a different computer. For example, different operating systems have different methods for rounding numbers. I generated output files for my code on my computer and moved the files to the test files folder.  Then I wrote a script that automatically compares output files produced by another user using my code on another operating system to the test files I produced using my code on my operating system.  If there are differences, then a user will be able to identify and address them.

The most critical step for archiving my code was writing the documentation (README file).  The documentation includes a description of the purpose of the code, references to research articles, a list of software dependencies including versions, clear step-by-step instructions on how to use the code, and clear step-by-step instructions on how to use the test files.  I also included a section to acknowledge my funding sources and others who helped with the project.

The final step was to submit the code to a long-term archive which keeps a permanent copy and notify the journal.  


##### Pain points

Archiving my code takes additional time.  

I complete the archiving process more efficiently now that I have established a workflow for making my code reproducible.

##### Key benefits
Reproducibility has always been an important component of research in my field.  In the past, instructions for reproducing research were put in a methods section in journal articles. The increasing importance of code in my field is changing the way reproducibility is accomplished because it is not possible to include code in a methods section.  However, it is necessary to have access to the code to reproduce the research.

My workflow is an example of a way to incorporate access to code into the overall publication process.  I make the process for making code reproducible similar to the process that is used to make experimental techniques traditionally described in a methods section reproducible. I think keeping the process as familiar as possible will be key for getting others in my field to provide reproducible code as part of the research publication process.

##### Key tools

I have always believed that making my code available is important, but, until recently, I was not sure how to do it. Github is a "game-changer" for sharing code with others in a reliable, consistent, and discoverable way. After I was introduced to Github, I was able to start archiving my code.  My code is posted to Github and a permanent copy and DOI are generated by Zenodo.

There are specific instructions on Github for releasing code to Zenodo:  

[https://guides.github.com/activities/citable-code/](https://guides.github.com/activities/citable-code/)  

##### General questions about reproducibility

1) Why do you think that reproducibility in your domain is important?

Reproducibility has long been a central tenet of the scientific research process in my field because data from new studies are compared to data from earlier studies.  Not so long ago, all the data collected during a study were included in published research articles, and the analyses could be easily described in a materials and methods section of the articles.  Recent increases in the quantity of data and the concurrent increase in the complexity of the analyses has made it impossible to include the data itself or the same level of descriptive detail in the materials and methods sections of research articles.  I think that my domain values reproducibility but the current format for publishing research articles is not able to fully accommodate the modern scientific research process.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

4) What do you view as the major incentives for doing reproducible research?

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?
