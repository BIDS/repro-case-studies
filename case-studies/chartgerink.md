##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

I am Chris Hartgerink, an applied statistician at Tilburg University specializing in detecting potential data fabrication in the social sciences and applying content mining methods. As a PhD. student I am hard at work developing myself as an academic and spend much of my time paying attention to my workflow during my research projects. My case study will revolve around an experimental project involving human participants.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

For me, reproducibility pertains to the reliability of research findings, which both includes direct reproducibility (i.e., can someone else reproduce the results by applying the described method to the same data?) and retest reliability (i.e., if we rerun the study, do we get similar results?). My case study will focus on direct reproducibility, that is, that anyone or a future-me can retrace the steps from the project in such a way that it is understandable and that the results are reliable.

##### Workflow diagram

[Diagram](chartgerink.pdf)

##### Workflow narrative

Upon idea conception of the experiment, an initial meeting is planned to sketch the idea of the project in more detail. This takes place as an informal meeting with as many members of the project as possible, but does not include a formal agenda. During this project description I will write from the perspective of the project lead who undertakes the steps described along the next few paragraphs. Despite the lack of a formal agenda several points are on my list to address during the "Idea sketching" meeting:

1. Agree that research files will be publicly shared by default and proper arguments are needed to *not* share research files publicly (e.g., ethics committee restraints).
2. Agree that the publicly shared research files are put in the public domain (licensed Creative Commons 0), to maximize breadth and clarity with respect to re-use rights of the research materials.
3. Agree that the research manuscript will be shared as a preprint upon completion, for improved peer feedback, and that the manuscript will be published openly and with an appropriate re-use license only (i.e., CC-BY or CC-0).
4. Role assignment within the project (e.g., who will be responsible for acquiring the necessary funds, who will analyze the data, who will check the analyses).
5. The actual idea sketching.

The "Idea sketching" meeting is followed up by the project-lead with a draft description of the project and an initial draft of the materials to be used. These contents include a technical description of the design, hypotheses and theoretical framework, but also a draft of how the data will be analyzed. This increases transparency in what methods are set out to be applied, and increases accountability amongst authors. Even if these methods seem obvious, explicating them is important because during this process questions often arise that are not so obvious from the start (e.g., are covariates included? Are covariates you want to enter actually measured in the study design?). These drafts are shared and iteratively revised until an agreed outline of the project is agreed upon. The experiment I describe here involves human participants and will need to be submitted to the ethical committee for review. Considering that each university has different procedures, I will not extend on these.

Note that the files that are drafted after the meeting are included in a [Github](github.com) repository, which allows for version control of the files and is synchronized to an Open Science Framework (OSF; [osf.io](osf.io)) repository, which provides a searchable index of scientific repositories. Version control can be compared to a track changes for computer files, allowing you to go back in time and view what changes were made and when. During this process, a logbook of changes is implemented, which improves the reproducibility of the research process if anyone is ever interested in that. My experience is that almost nobody outside the research group typically is, but it can serve as a handy reference when somebody asks you for specific dates, such as when the sampling frame was collected. Version control starts after the "Idea sketching" meeting in my proces, but can also be implemented any other time prior to preregistration.

The version controlled research files are preregistered after ethics approval is acquired and potential revisions are incorporated. This preregistration is done on the OSF, which is done with the click of a button. This preregistration makes an unalterable snapshot of the research files with a timestamp, which serves as a way of indicating that your hypotheses were developed prior to the analysis of the data and are truly confirmatory.

Following the preregistration, it is time to actually conduct the study. During this time, it is also a good time to rewrite the preregistration in such a way that the introduction and method sections of the manuscript are already done. It is possible to write your preregistration in such a way that it already resembles these sections, but I typically try to be more detailed in the preregistration and subsequently prune it into the manuscript, containing the most vital elements.

When the study has been conducted, the raw data need to be stored in a non-proprietary file format and stored as read-only files. Creating back-ups is trivial when you use the OSF/Github, because you have online back-ups. However, it is important to ensure the file is read-only, so you do not accidentally overwrite the file. Saving the raw data as a non-proprietary format means that you should not save it as an SPSS, Excel, or other commercial format. This is of utmost importance, because if you do it is likely you will not be able to process the data in, for example, 10 years. The best types of file formats are those that store the data in a raw text format like Comma-Separated Value files (.csv) or tab delineated text files. Moreover the people who do not own these commercial software packages can still read the data, and you do not force them into your software approach (e.g., there are researchers who strongly feel that all software used by researchers should be publicly available for inspection of the source code, including myself).

Upon having safely stored the data, it is time for data to be cleaned in an automated, scripted manner and followed by the analyses themselves. I typically conduct my data cleaning and analyses in the `R` package, which is open-source software and allows you to create code that results in directly reproducible research results. I try not to clean data by hand, because I often forget I have done this. If I do need to do this, the logbook provided by version control is a safety measure and allows the logging of this. A best practice is to make the script standalone and read in the dependencies, such as a data file, from online resources (one example where I do this is available at osf.io/pvrtx). This ensures that the script is all that is needed to reproduce the analyses.

Upon completion of the analyses and incorporating the results, the co-author (or co-authors) assigned with checking all the analysis code is given all research files and checks whether the research results in the manuscript correspond to the analyses themselves and whether the analyses were run correctly (i.e., co-piloting). Typically, some discrepancies such as rounding errors or unclarities in the scripting do occur, but worry not: this is exactly why this check occurs. These errors are subsequently revised and potentially checked again, if the errors were substantial. I typically do a final check to see if the numbers indeed correspond and whether I can run all analyses with just the script without altering any of the parameters. If so, I update the files in the version control and check whether they are publicly available, prior to submitting the manuscript (I have left out the writing process somewhat at the end of the workflow, for parsimony sake).

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

The part of a reproducible workflow that I consider particularly painful is that of co-piloting analysis scripts. It shows clearly when a researcher is reproducible, but most often shows how it is still lacking. As a result, it can sometimes take an entire day to check the analyses a colleague has done on a project. However, when reproducibility increases, co-piloting also becomes less strenuous. Additionally, knowing the particularities of checking other people their work helps improve reproducibility of your own work, by increasing what aspects are important to get right. This is why I go through hoops to make sure *one* file is sufficient to get all the results in the manuscript and that dependencies or datafiles do not cause any trouble.

Another aspect of a reproducible workflow is that it comes down to the project lead to enforce reproducibility, most often. I want my research to be reproducible, so I enforce this in my project. Co-authors need not have the same perspective on this and therefore you have to ensure that what they do is reproducible as well. If the project has a centralized project lead, who coordinates everything, this is less of a problem, but with more decentralized projects it can cause some haphazard. It requires you to structure the project, which is a good thing, but can require substantial effort when projects get increasingly complex (note that increasingly complex projects also have a higher need for reproducibility because of a higher potential for error-making).

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

My workflow has actively developed in recent years and one of the aspects I am most proud of is that, since the summer of 2015, I have created analyses scripts that can run alone, requiring the reproducer to only download that script and nothing else. It can be quite daunting when a researcher shares ten files and you have to find a way through them. It is not sufficient to be transparent to become reproducible, but it is highly important to structure your documents so that others, including your future-self, can understand what is going on.

Using version control is an active benefit, which my direct colleagues are starting to realize as well, due to my efforts to get them to use it. It is affirming to hear them stress that they enjoy using it, because it helps them increase efficiency in the long run despite costing some time to learn. It is a tool that provides an individual researcher with the least costly way to become reproducible, but still requires some effort in the beginning because it is a change. So it seems that there is substantial benefit that improves the research process and I hope that other colleagues will see the value in that sooner rather than later, when their data gets audited.

##### Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*

I use a set of tools, which all have one thing in common: they are based on open formats that are timeless, inclusive, and can be used by anyone who has a computer. These open formats include the data in tab delineated text files, but also includes software packages that are open-source and whose code is checked by the open-source and academic community (e.g., `R`, `git`). It seems to me that the use of closed software has proliferated throughout the social sciences (in which I operate most of the time) without the realization that it is actually hurting the future of science (e.g., irreproducibility of results), but also hurts current-day science. Not everybody can afford a license to SPSS or Microsoft Office, for example. Why exclude those who do not have those funds? Science is an enterprise that should be all-inclusive and not select on financial wealth of individuals or institutions. I try to reaffirm this principle by ensuring that all the tools I use are open-source and can be used by anyone who wants to.

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

Scientists are humans and humans make mistakes. By using reproducible practices, we can discover these mistakes and not be led down a research path that is based on a mistake. It is important in my domain, because we preach that results contain errors, which makes it highly important that I make as few errors as possible.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I got interested in reproducible practices during my master education when my supervisor introduced me to the OSF. I found myself wondering how to implement it in different stages of the research process, not knowing where to start documenting *during* the research. I learned much from colleagues across the world and across fields with who I discussed ways to be more reproducible over social media (mostly Twitter, which is a highly valuable resource for researchers).

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

Reproducible research is tiresome when you figure out a new way of doing things and then think that your previous work is incomplete. Additionally, not all colleagues are as enthousiastic as myself and this can lead to discussions (also a good thing) that postpone implementing certain practices. It is very important to get everyone on the same page in the initial meeting on how the project will be managed, such that nobody is met with surprises and potential ambivalence at the end. This is why I have the "Idea sketching" phase include these steps.

4) What do you view as the major incentives for doing reproducible research?

The main incentives for reproducible research is (future) efficiency. When you know that you can revisit projects from a month or years ago and only needing at most 30 minutes to find what you are looking for is a major improvement over spending a day looking for that one specific value someone asked about in your email. It also helps revisit previous projects and see what I did, because sometimes I unlearn things I require in a new project (e.g., I often forget how to make plots in the `ggplot2` package because I use it too infrequently, and I just reuse code from a previous project).

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

The best practices I recommend any researcher to apply are the following:

1. License your work with an open license (CC-BY or CC-0), explicating free re-use of your materials and manuscript.
2. Script your data handling and analyses as much as possible, such that each step is reproducible.
3. Have a colleague check your analysis code, it is too easy to make mistakes. Not checking analysis code is comparable to not having co-authors proofread the manuscript.
4. Try and create an analysis script that can run automatically, downloading all required files and installing its dependencies. Otherwise, other people are likely to fail in reproducing your results, when they cannot get to the dependencies.

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

I recommend the research paper by Karthik Ram on using version control in research. It was an eye-opener for me on the use of project management tools to improve reproducibility at the lowest cost possible. The OSF also has training tools online, which can be found on their website (osf.io).

Ram, K. (2013). Git can facilitate greater reproducibility and increased transparency in science. Source Code for Biology and Medicine, 8(1), 7.

### Potential conflicts of interests
Chris Hartgerink is a Center for Science ambassador.
