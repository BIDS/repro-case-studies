##### Title

A Statistical Analysis of Salt and Mortality at the Level of Nations

##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Kellie Ottoboni. I'm a PhD student in the Department of Statistics at UC Berkeley. My research focuses on nonparametric statistics, causal inference, and applications in health and social sciences. The project I describe in this case study is an investigation of the association between salt consumption and mortality at the level of nations.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

I think that a data analysis project is reproducible if there are enough breadcrumbs (in the form of code and instructions) for anybody to recreate the analysis from start to finish.  In another sense, a project is reproducible if someone can carry out a different analysis on the data and arrive at qualitatively similar conclusions.

##### Workflow diagram

The core of your case study is a visual diagram, and associated textual narrative, describing the workflow for your case study.

Begin by creating a diagrammatic sketch, which you are welcome to do by hand, that shows your workflow pipeline visually. If you would like to do this digitally, we recommend the site draw.io.

Think of this like a circuit diagram for your workflow. Boxes should represent individual steps in the process, with arrows showing how the inputs and outputs of each step relate to each other. Be sure to consider

* specialized tools and where they enter your workflow

* the "state" of the data at each stage

* collaborators

* version control repos

* products produced at various stages (graphics, summaries, etc)

* databases

* whitepapers

* customers (if any)

There are two examples diagrams attached with this template for reference.

Please save your diagram alongside this completed case study template.

##### Workflow narrative

Referring to your diagram, describe your workflow for this specific project, from soup to nuts. Imagine walking a friend or a colleague through the basic steps, paying particular attention to links between steps. Write this description in text. Don't forget to include "messy parts", loops, aborted efforts, and failures.

It may be helpful to consider the following questions, where interesting, applicable, and non-obvious from context.

* For each part of that workflow:

    * How often does this step in the workflow happen?

    * How long does it take?

    * Which members of your team participate (or not)?

    * How much human intervention is involved?

        * Is that human intervention recorded in some way?

    * How much is scripted or otherwise automated?

        * What records are kept about this automation process?

    * Which software or online tools do you rely on?

        * What are its key important uses and limitations?

        * Does it make you more efficient or slow you down?

        * Does this tool affect your ability to reproduce your results?

        * Have you previously tried any other tools for this task?

        * Are you aware of tools that might make this step more efficient? If so, why have those tools not made it into your workflow?

    * How opaque is this step to a researcher external to your research group?

        * Is the necessary code online?

            * How is the documentation?

            * Are there tests?

            * Do you keep example input files alongside your code?

        * Is your raw data online?

            * Is it citeable?

            * Does the license allow external researchers to publish a replication/confirmation of your published work?

        * Is your data processing workflow online?

            * Are the scripts documented?

            * Would an external researcher know what order to run them in?

            * Would they know what parameters to use?

I became involved in this project after our collaborators at UC Irvine had begun putting together the dataset. The data consists of demographic and socioeconomic variables, as well as gender-specific estimated sodium, alcohol, and tobacco consumption for 38 countries. The data were pulled together from a variety of sources and the variables are described in a codebook file.

The first step was to decide what data we needed to answer the question: does salt consumption have an effect on a nation's life expectancy at age 30? We decided that the best way to address this would be to consider males and females separately, and to use a country as its own "control" by looking at the changes in life expectancy, alcohol, tobacco, and sodium consumption, and economic variables over time. We had the variables we needed, but gender-specific alcohol data were missing for one year. These couldn't be obtained so we imputed them based on gender ratios in each country and overall consumption that year. We also had to remove countries with missing data on life expectancy, the outcome of interest. I documented these steps in a LaTeX report as I went along.

The method of analysis was a novel approach that we have been developing. The premise of the method is to predict the outcome of interest, change in life expectancy, as well as possible using all covariates *except* the treatment of interest, sodium. If sodium is related to life expectancy, even after controlling for known health predictors, then sodium consumption will be associated with the residuals of the model. This is a tautology: if sodium is associated with life expectancy but we exclude it from the model, then some of the variation that the model cannot explain will be associated with sodium (assuming that sodium is not perfectly correlated with the covariates we include in the model). But how large of an association is statistically significant? We answered this question using nonparametric permutation tests. After discussing how our approach might answer the problem at hand, I wrote R code for the two main steps in the algorithm: the model selection and the nonparametric test of association. I have an existing R package for our proposed statistical method in a public GitHub repository, so I added this code and documentation into the package. I developed the code iteratively by running it on our dataset and checking that the format of the output looked sensible.

After writing each component of R code, I combined all of the preprocessing, analysis, and plot scripts into an R Markdown file. KnitR allows you to compile R Markdown, R code chunks interleaved with markdown text, into a PDF or HTML document. This way, I could send my collaborators the results quickly and in a user-friendly format. I posted all the scripts, data, and the compiled HTML document in a public GitHub repository dedicated to this project.

At this point, we were unsatisfied with the scope of the analysis and wanted to ask more questions. In particular, we wanted to run the same test of association with life expectancy, but using tobacco and alcohol in place of sodium. These analyses would serve as a "sanity check" that the method performs as expected. Given that we know that both alcohol and smoking have negative effects on health, we would expect to find a negative association between the model's residuals and alcohol and tobacco use. The original dataset included alcohol consumption per capita, but no measures of tobacco use. This required our collaborators at UC Irvine to gather this data from an existing journal article. After receiving the tobacco usage data from them and performing the model-based matching analysis with it, we realized that the measure of smoking that we had was not a good measure of a nation's overall tobacco use. We again gathered different tobacco data and ran the analysis one last time. Since the R scripts had already been written, redoing the analysis with each version of the data amounted to changing a few lines of code, so the process was relatively painless. I kept each version of the data used and named them according to the date which it was sent to me.

We believe that we have done all the statistical analysis that we need to answer the scientific questions that we posed.  The analysis portion of the project took about six months to complete. Our collaborators are preparing a manuscript. We are using LaTeX and communicating by email.

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*

A seemingly trivial problem I struggle with is keeping track of files. Using git certainly simplifies the version control aspect of file organization, but that doesn't help when I've forgotten where I put a chunk of code I wrote two weeks ago. Around the beginning of this project, I started keeping a "lab notebook" to organize my thoughts on all the various projects I'm doing. I keep a folder of text files just for myself where I jot down the date, ideas and concerns, notes on what work I've done, and the names of files or folders where I saved that work. It has helped tremendously when I need to remind myself things about a project, and it's also a nice way to archive meeting notes and save ideas that I might want to share with collaborators later on.

A pain point particular to this project was trying to encourage my collaborators to use the GitHub repository. Because of the learning curve to start using git, we ended up sending data and results back and forth by email. Since I put all the files on GitHub anyway, sending the results to collaborators was just duplicated work. I would have appreciated having the updated data files simply pushed to the repository along with scripts used to gather the data.

The data collection part of the project was opaque. Our repository does not include any scripts used to collect the data from various databases and journal articles or scripts to merge these data sources. At one point, under pressure of a deadline, I manually entered tobacco consumption figures into an Excel spreadsheet. All the preprocessing and analyses of the data are reproducible, but the process of collecting the data is not.

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example?*

I am proud of the R tools I used in this project. This was my first time using KnitR and I am pleased with documents I created to share the results with my colleagues. All steps of the data analysis are in the documents, alongside my commentary and explanation of the steps. I hope that this makes my workflow transparent to my collaborators so they don't feel like all the statistics were done in a black box. Additionally, having all the tables and figures in one place will make it easy to put results into the manuscript. 

Incorporating the main functions for this analysis into an R package with larger scope will be beneficial in the future. Often, statisticians write one-off scripts and neglect to document their code, making it a challenge for anybody else to use it. In contrast, the functions I wrote for hypothesis testing here are well-documented and uniform in their style, inputs, and outputs. Having them all in a package on GitHub makes it easy for anybody who reads our paper to install the package and replicate our results.

##### Key tools [Optional]
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience.*

[Answer, 200-400 words]

##### General questions about reproducibility [Optional]

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

Researchers tend to blame the "reproducibility crisis" on statistics, and in particular p-values. It's our job as statisticians to fight this claim by making statistical analyses as correct and as transparent as possible, so people know exactly where their p-values are coming from.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I learned some of these practices from other students in my department and the rest were self-taught using resources on the internet.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

[Answer]

4) What do you view as the major incentives for doing reproducible research?

[Answer]

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

Explain every step in the data preprocessing and analysis carefully and thoroughly. Document and comment code liberally. Make code and data publicly available.

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

Hadley Wickham's *R Packages* book is an invaluable resource. He demystifies the R package and shows how to use RStudio to make the workflow smooth and efficient.