##### Introduction

K.A.S. Mislan
Postdoctoral Associate
eScience Institute  
School of Oceanography  
University of Washington

I am an ecophysiologist and my research focuses organism-environment interactions in the ocean.  In particular, I am interested in forecasting the effects of climate change on marine ecosystems.


Reproducibility means that sufficient descriptive information and resources are provided for someone to be able to repeat the same study. As part of my research as a scientist, I write code to manipulate and visualize large quantities of data to obtain results. I believe that my code should be adapted and made available so that it is usable by others in my field.

##### Research workflow diagram

![Research Workflow](kasmislan_researchworkflow.pdf)

##### Research workflow narrative

I recently completed a project on blood-oxygen binding  in the global pelagic ocean. In this narrative, I use the project as an example to explain my research and reproducibility workflows. The data for the project came from existing resources. Obtaining the data from the existing resources is the first step in my research workflow.

World Ocean Atlas 2009 (WOA09) data is publicly available through the National Oceanic and Atmospheric Administration (NOAA) National Centers for Environmental Information. The WOA09 data is on a geographic grid and available in several different file formats. I downloaded the netCDF (.nc) file format because the netCDF files are relatively small in size and tools are available to read and manipulate the files. NOAA Ferret is publicly available software for visualization and analysis and has built-in functions designed for efficient processing of gridded data. One of the objectives of the analysis was to vary two input parameters and determine the effect on a geographic characteristics. I automated the process of creating ferret scripts with different input parameters by writing a shell script that generated and processed ferret scripts (.jnl files).  The processed files were saved as netCDF files.  

R and Python were used to create the figures although it would have been possible to create all the figures in one or the other of these software packages. I learned R before Python so I tend to do most of my analysis in R because I am most familiar with it.  However, I like the tools for making geographic plots in Python so I used Python to make the geographic plots.  

The physiological data was gleaned from published studies found through Google Scholar searches for key words. As the data was extracted from the papers, it was put into a spreadsheet. The data of interest was often available in tables and the text of the papers. In some cases, the data was only available in scatter plots.  The ruler tool in Adobe Photoshop was used to manually extract the data from plots. Once all the information from the studies was entered into the spreadsheet, the data from the spreadsheet was saved as a tab-delimited text file. The data was then read into R to determine parameters for the analysis of the oceanographic data.  Additionally, the data was plotted in a scatter plot in R and each point in the plot had a number assigned to it. Information about the individual points was put into two tables. However, it was inefficient to obtain the information by looking between the numbers on the plot and the two tables.  Therefore, an interactive plot that includes the information from the tables was created using D3.

I created figures and wrote the paper.  It was not possible to include the steps associated with the code in the methods section of the paper due to space and formatting constraints. However, the code tells a much more complete story of my analyses.  I adapted the code and provided documentation so that the code could be used by someone else in the same way that I used it in my study. Therefore, I changed as little of the code as possible when adapting it to be independent of my operating system.


##### Reproducibility workflow diagram

![Reproducibility Workflow](kasmislan_reproducibilityworkflow.pdf)

##### Reproducibility workflow narrative
I have developed a workflow for converting my research workflow to be reproducible.

##### Pain points

For me, the most painful step in my reproducibility workflow is getting started. My research workflow is motivated by my interest in addressing a scientific question and therefore is exciting. Comparatively, my reproducible workflow is boring because it is routine. Also, once I am ready to begin the reproducible workflow, I am working on new scientific questions which I gravitate towards when I am deciding how to spend my time.  

Now that I have an established workflow for making my code reproducible, I have an easier time getting started because I know where to start, and I complete the process efficiently.

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

- focus on science first

##### Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*
- Github  
- Zenodo

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

Reproducibility has long been a central tenet of the scientific research process in my domain because data from new studies are compared to data from earlier studies.  Not so long ago, all the data collected during a study were included in published research articles, and the analyses could be easily described in a materials and methods section of the articles.  Recent increases in the quantity of data and the concurrent increase in the complexity of the analyses has made it impossible to include the data itself or the same level of descriptive detail in the materials and methods sections of research articles.  I think that my domain values reproducibility but the current format for publishing research articles is not able to fully accommodate the modern scientific research process.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

4) What do you view as the major incentives for doing reproducible research?

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?
