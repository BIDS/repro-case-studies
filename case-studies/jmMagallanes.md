##### Introduction

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

I am José Manuel Magallanes. From 2015 - 2017, I am a Senior Data Science Fellow at the eScience Institute of the University of Washington, where I am also a Visiting Professor at the Evans School of Public Policy and Governance. Since 2003, I am Professor of Political Science and Public Policy Methodology at the Catholic University of Peru. My research is related to framing political and policy problems with a computational social science approach. I have dealt with different topics including electoral behavior, public management performance, climate change and social conflict, and Congress's legislators behavior. My contribution for this case will be a research carried out on bill consponsorship data to detect key players, reveal association patterns, anticipate party splitting and detect tactics to be re elected. 

I have a BSc in Computer Science, a MA in Political Science and Public Management, a Phd in Psychology and a Phd in Computational Social Science (George Mason University).

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In general, I consider this term means the level of reconstruction of a research that can be achieved by a person foreing to the researcher / research team via the code and data available in some repository. For me, reproducibility is not only that the foregin person can decompress and run and exceutable file to see the results, but be able to audit the whole process. The less feedback required by the auditor, the more reproducible a  work is.

##### Workflow diagram
![image](Diagram_jmMagallanes.png =800x500)

##### Workflow narrative

The workflow above represents:

a. Manual Stages:
	1. Define the Research Problem.
	2. Design the Research Plan.
	3. Review the Literature.
	4. Paper writing.
	
b. Automated Stages:
	1. Data compilation.
	2. Organization of References.	
	3. Updating computations and plots.
	4. Paper production and updating.
	5. Organization of archive.
	6. External User interface.

##### A. Manual Stages	 
a1. **Defining the research problem.** There was an interest in the political science community to learn more on the dynamics of the Congress. There were some particular facts that have been discussed in academia and in the media that called our attention:

* The low re election rate of congressman the previuos two elections (20%).
* The fact that some congressmen migrated to other parties during their mandate (party switching).
* The fact that parties that have a good share of seats, end up splitting their seats (It is worth keeping in mind that Peru has a multiparty system).

The fact that some scholars in the USA were using bill cosponsorship data as a proxy to understand some of these issues, motivated me to follow a similar approach.

This stage was done only once. I was the only one in charge. No particular tools was used in this stage.

a2. **Designing the Research plan**. This stage identified the main authors that have worked similar research problems before. The key ingredient in all cases were bill cosponsorship. However, most hypothesis were not the same I had due to the different political regime. But, in all cases, bill cosponsorship was consider a good proxy to understand legislator's associative patterns. Fron this stage it was clear that:

* There will be a need to producing some coding to extract the information from the Congress of Peru website, as the data is not available for download by any means.
* To test the hypothesis, it will be needed the information of a complete Congress (five years).
* The information form the bill cosponsorship will need to be complemented with the Archives of the National Jury of Elections. There, personal information on every Congressman is available. This information was shared, so no code was need to collect it.
* There will be a need for graph or social network techniques.
* The budget available will require the use of free tools.
* There will be a need to share the findings with other scholars.
* This research could be combined with other efforts in another similar countries. So there was a need to organize effciciently the process so that data and code could be re used.

This stage was done only once. I was the only one in charge. No particular tools was used in this stage.

a3. **Review of the literature**. This step allow me to identify similar cases and organize ny basic set of references. The references were continously updated along the process. I was in charge of upating, but also got some recommendations from the user I shared my drafts with.

a4. **Paper writing**. As expected, this was a manual step. However, as I will describe later, this was supported by different tools. As usual, this step was repeated many times. I was the only contributor.  

##### B. Automated Stages	 

b1. **Data compilation**. The data is available at: <http://www.congreso.gob.pe/proyectosdeley>. However, the webpage does not offer an API or a possibility to download the data in a structured way. For this reason, a code for scrapping the website was needed. The code was written in Python, relying mainly on the beautiful soup package. There were some extra code to clean the values collected. The electoral Archives had data on the legislators themselves. The data was merged with the data scrapped. Python was used to generate two files: a data frame for the legislators and a network of cosponsorship among them. The files were save in the working folder and exported in formats readable by R.

This process was done entirely by me. It was the first part of the operational research and took around two weeks. The Python version I used was 2.7, and it was installed via Anaconda. I used the Spyder-app GUI to do the coding.

b2. **Organization of references**. References included webpages, white papers, code, data, and so on. For their organization, **Zotero** was used. It allowed to create a bibTex file to be used later during the paper production process. 

This process was done entirely by me. This was a continuos process as the paper was written. The desktop version of Zotero was used. The Bibtex was saved in the working folder.

b3. **Updating computations and plots**. From the hypothesis, the research plan and the data collected, a set of statistical modeling functions were coded in R under RStudio. A *sweave* document was produced to send R chunks of code into Latex. 

This process was done entirely by me. This was a continuos process as the paper was written. A Rnw file was produced using RStudio, which also produced a Latex file. 

b4. **Paper production and updatings**.  The paper integrated my writing, the bibliography file, and the tables and plots generated from RStudio into a Latex document. Any change in whatever of this documents updated the whole product automatically. 

This process was done entirely by me. This was a continuos process as the paper was written. Latex complied the R chuncks producing tables and plots, and compiled the bibliography unto the main document from the BibTex file generated in Zotero.

b5. **Organization of archive**. One of the first steps after the research questions were clear, and before any coding was made,  was the creation of a **GITHUB** private repository. This repository was cloned into my laptop, and all the files were organized in this folder, including code, data files and plots. 

This process was done entirely by me. This was a continuos process as the paper was written. The GITHUB client was used for comitting and synchronicing the local repository into GITHUB. 


b6. **External User interface**. In was clear during the planing stages that I will need to share my drafts with other colleagues in order to get some feedback and/or discuss further collaboration on this matter. As the paper reflected an step-by-step approach, it would be easier for my collegues to read the draft paper which included the code chuncks, the plot and the tables. For that, I decided to use **ShareLatex**, which can collect the files in the GITHUB repository and compile the Latex document. 

This process was done entirely by me. However, the drafts were shared when most of the processing was finished. This was a continuos process as the paper was written. The selected users created ShareLatex accounts to see the Latex generated pdf version of my document. I allowed them to write comments in the Latex document usign ShareLatex itself.

##### C. On the Data, Softwarer and Processing

* **Data:** The raw data as well as the cleaned and aggregated data are online, in a private Github repo. The data can be share upon request and instructions are included on how to cite it.

* **Software:** The Python code is also in the repository. The R code is embedded in the Latex code, and the paper itself describes the algorithms adopted in the paper. Most R chunks make constant use of the data dta Python scrapped.

* **Processing:** The processing of the data is reflected in the Python code flow, and it is online. The Python and R codes are commented extensively. It would be fairly easy for an external researcher to follow the logic of the reserach and replicate the results, or simply change the data from other country and get all the tables and plots in the final PDF, as R, Python and Latex are connected.


##### Pain points
This works was not producing a blog, or a notebook but a paper. So the most challenging part was to produce a good version where tables and plots are located in the rigth place. Fortunately, Latex had enough flexibility for that. However, finding the right packages and commands in Latex took lot of time. For the data scrapping, I muste mention that Python worked very well, but still you need to find out how to add some simple configurations when visiting multiple webpages. This is a small configuration that took too much time to identify. A particular pain point is the lack of a reproducibility culture in the field I work. Political scientists in my country are not used to reproducible research. In fact, for every key paper that dealt with the kind of data I used, no further instructions were found from the authors or in the authors' webpages. In most cases, it is only mentioned what data was used but no links or other related procedures were clear.

##### Key benefits
Planing your research in a reproducible way is a great advantage to the scientific community you belong to. But most of all, it forces you to plan your work better. If you work as I did, including a GitHub repository is even better, as you shoild plan since the begining the folder structure in your work. Following a reproducibility approach will allow you scalet your work if more data becomes available or if a colleague wants to make a comparative work. I am sure this is not impossible without this approach, but I am sure that researchers can become much more productive than in the past.
Another important benefit is that allowing colleagues auditing your work gives you enough input to make a newer and more robust veesion of your work.


##### Key tools
Latex was a key component in all this research and its reproducibility level. It offers a way to organize the paper and interact with code and data files, including references and plots. This can not be done using Word, as far as I know. Latex is not a common software in social scientists in my country.
RStudio is also a key ingredient. Its capacity to transform the R chunks and its output (including tables, values and plots) into Latex makes the flow and update of research even better.
Both Latex and RStudio facilitate reproducibilty. Without R, the barrier for producing papres is even higher, but it can be done. It gives you more confidence and save you lots of time to update/edit your manuscript, compare to copy, past or inserting procedures in MsWord. The flow is simply great. 

##### General questions about reproducibility

1) Why do you think that reproducibility in your domain is important?

* Because computational social science is still young in many other countries. As in my case, data is just starting to become available, so following, and teaching, the reproducibility approach will benefit the research quality. In public policy, particularly, it will favor stake holders participation in knowledge creation.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

* I had no chance to have mentor or courses on this. I just felt the need to organize my work as many tools and data were available for my case. I was afraid that if I did not follow this approach I could easily get lost. Reproducibility request good research planing, and it pays off. 

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

* If the data you are using is public, I see *less* problem. When the data is not, and you get access with a special permission, legal issues are always present. As for investment, my particular collection of tools are free, so it should not be a problem, unless your funding institution forces you to use particular tools. I also believe that this approach can be very challenging for older generations not used to this. I see less of a problem in youger generations of researchers.


4) What do you view as the major incentives for doing reproducible research?

* That it allows you to improve your work.

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

* I could only share this experience.

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

* Not now.

