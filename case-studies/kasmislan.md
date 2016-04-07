### Title for Case Study

K.A.S. Mislan  
Postdoctoral Associate  
eScience Institute  
School of Oceanography  
University of Washington

##### Introduction

I am an ecophysiologist and my research focuses organism-environment interactions in the ocean.  In particular, I am interested in forecasting the effects of climate change on marine ecosystems.

Reproducibility means that sufficient descriptive information and resources are provided for someone to be able to repeat the same study. As part of my research as a scientist, I write code to manipulate and visualize large quantities of data to obtain results. I believe that my code should be adapted and made available so that it is usable by others in my field.

<!---- Description of case study... -->
I recently completed a project on blood-oxygen binding in the global pelagic ocean.  

**Research Paper**:  
Mislan, K. A. S., Dunne, J. P. and Sarmiento, J. L. (2016), The fundamental niche of blood oxygen binding in the pelagic ocean. Oikos. doi: [https://doi.org/10.1111/oik.02650](https://doi.org/10.1111/oik.02650)

**Code Archive**:  
Mislan, K. A. S., Dunne, J. P. and Sarmiento, J. L. (2015). P50 Depth Analysis v1.0. Zenodo. [http://dx.doi.org/10.5281/zenodo.31951](http://dx.doi.org/10.5281/zenodo.31951)

##### Workflow diagram

![Research Workflow](kasmislan_workflow_v5.pdf)

##### Workflow narrative

Obtaining data from existing resources was the first step in my research workflow for this study.  World Ocean Atlas 2009 (WOA09) data is publicly available through the National Oceanic and Atmospheric Administration (NOAA) National Centers for Environmental Information. The WOA09 data is on a geographic grid and available in several different file formats. I downloaded the netCDF (.nc) file format because the netCDF files are relatively small in size and tools are available to read and manipulate the files. NOAA Ferret is publicly available software for visualization and analysis and has built-in functions designed for efficient processing of gridded data. One of the objectives of the analysis was to vary two input parameters and determine the effect on geographic characteristics. I automated the process of creating ferret scripts with different input parameters by writing a shell script that generated and processed ferret scripts (.jnl files).  The processed files were saved as netCDF files.  

R and Python were used to create the figures although it would have been possible to create all the figures in one or the other of these software packages. I learned R before Python so I tend to do most of my analysis in R because I am most familiar with it.  However, I like the tools for making geographic plots in Python so I used Python to make the geographic plots.  

The physiological data was gleaned from published studies found through Google Scholar searches for key words. As the data was extracted from the papers, it was put into a spreadsheet. The data of interest was often available in tables and the text of the papers. In some cases, the data was only available in scatter plots.  The ruler tool in Adobe Photoshop was used to manually extract the data from plots. Once all the information from the studies was entered into the spreadsheet, the data from the spreadsheet was saved as a tab-delimited text file. The data was then read into R to determine parameters for the analysis of the oceanographic data.  Additionally, the data was plotted in a scatter plot in R and each point in the plot had a number assigned to it. Information about the individual points was put into two tables. However, it was inefficient to obtain the information by looking between the numbers on the plot and the two tables.  Therefore, an interactive plot that includes the information from the tables was created using a javascript library called Data-Driven Documents (D3).

I created figures and wrote the paper.  It was not possible to include the steps associated with the code in the methods section of the paper due to space and formatting constraints. However, the code tells a much more complete story of my analyses.  I adapted the code and provided documentation so that the code could be used by someone else in the same way that I used it in my study. Therefore, I changed as little of the code as possible when adapting it to be independent of my operating system.

 I made some modifications to the code at the time

 In this study, projects tend to involve large quantities of data which can take hours or days to analyze There is a lot of repetition in my use of code during projects. My goals in providing code is that someone can get the code working in a short period of time and understand the code under the simplest conditions.  Therefore, my first step is to select example data files for analysis and/or a small set of parameters for model simulations. In other words, I stray from exact reproducibility at the level of the project but not at the level of the code in order to make my code more "user-friendly".

The next step is to create (or modify) a folder structure. The folder structure needs to include a folder for code and folders for any additional auxiliary files including input files to run the code and output files produced by the code.  There also needs to be a folder for test files to determine if the code worked.  This organization of folders helps me because I am able to refer users of the code to file locations when I write documentation for the code.  

I annotate my code while I am writing it, but the annotations are usually short and meaningful only to me.  In my reproducibility workflow, I add descriptive annotations to the code. I also simultaneously change the file paths to be referenced solely within the folder structure (../../) so that the code is independent of my home directories (/Users/kasmislan/code/project).  

My code works on my computer, but it might not work the same way on a different computer. For example, different operating systems have different methods for rounding numbers. I generate test files for my code on my computer and move test files to the test files folder.  Then I write a script that will automatically compare output files produced by another user using my code on another operating system to the test files I produced using my code on my operating system.  If there are differences, then then it will be possible to quickly identify and address them.

My code depends on the installation of software programs including R and Python. Creating a list of these dependencies is necessary because they need to be installed for someone else to use the code.  These programs are updated so it is important to find out the versions.

In my opinion, the most critical step in my reproducibility workflow for making my code reproducible is writing the documentation (README file).  The documentation needs to include a description of the purpose of the code, references to research articles, a list of software dependencies, clear step-by-step instructions on how to use the code, and clear step-by-step instructions on how to use the test files.  When the data or parameters were reduced in size or number, I indicated that reductions have been made at appropriate points in the documentation.

The documentation can include additional components which are worth mentioning but not necessary for making research reproducible.  I include a section to acknowledge my funding sources and others who helped with the project.  In some cases, the code can be adapted for other applications so I often include instructions for modifying the code.

The final steps in the process of making my code reproducible are to request code reviews, fix bugs in the code found by the reviewers, and release a version of the code to a repository.  The code should be submitted to a repository which keeps a permanent copy and generates a permanent digital object identifier called a DOI (e.g. Zenodo).  


##### Pain points

For me, the most painful step in my reproducibility workflow is getting started. My research workflow is motivated by my interest in addressing a scientific question and therefore is exciting. Comparatively, my reproducible workflow is boring because it is routine. Also, once I am ready to begin the reproducible workflow, I am working on new scientific questions which I gravitate towards when I am deciding how to spend my time.  

Now that I have an established workflow for making my code reproducible, I have an easier time getting started because I know where to start, and I complete the process efficiently.

##### Key benefits
Reproducibility has always been an important component of research in my field.  In the past, instructions for reproducing research were put in a methods section in journal articles. The increasing importance of code in my field is changing the way reproducibility is accomplished because it is not possible to include code in a methods section.  However, it is necessary to have access to the code to reproduce the research.

My workflow is an example of a way to incorporate access to code into the overall publication process.  I really like that my research workflow allows me to focus on science first.  My reproducibility workflow then provides a path for me to transform my code to be reproducible when I am documenting my project for publication.  I tried to make process for making code reproducible similar to the process that is used to make experimental techniques traditionally described in a methods section reproducible. I think keeping the process as familiar as possible will be key for getting others in my field to provide reproducible code as part of the research publication process.


##### Key tools

I have always believed that making my code available is important, but, until recently, I was not sure how to do it. Github is a "game-changer" for sharing code with others in a reliable, consistent, and discoverable way. After I was introduced to Github, I was able to develop my reproducibility workflow.  My code is posted to Github and a permanent copy and DOI are generated by Zenodo as the final step in my reproducibility workflow.

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
