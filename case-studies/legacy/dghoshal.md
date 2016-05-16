
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

I am Devarshi Ghoshal, a postdoc researcher in the Computational Research Division at LBNL. I have a background in provenance capturing mechanisms and to use provenance for reproducing computational data.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

Reproducibility to me, is to generate the published/claimed results "as-is", given the set of input data and the code that generated the results based on the input data. 

# Workflow

[Diagram](https://github.com/dghoshal-lbl/repro-case-studies/blob/master/case-studies/dghoshal.pdf)


The workflow described here describes the research underlying provenance capture from network logs in order to understand task distribution, allocation of network resources and diagnose reasons for failures. A tool was specifically developed for capturing provenance from network experiments running on PlanetLab. By capturing the provenance information, scientists could understand the source of their outputs and the resources used for generating them. The goal of the research was to minimize experiment overheads, and provide a rule-based mechanism to capture provenance without instrumenting the experiment code. The research also resulted in a viability study of using rule-based log mining for provenance capture (doi:10.1145/2457317.2457366). 

The tool developed for this research, called NetKarma, is a component of a provenance capture framework, called Karma. It used the logs from Gush, a tool to control the application execution lifecycle that acted as a middleware for deploying and running applications on PlanetLab. The major change that used to happen frequently was the change of rule files. Ironically enough, it was not because of application changes but because of frequent changes in the logging mechanism of Gush. This would often result in re-writing the rule-files, becoming a major hindrance in reproducing the results. The version of Gush and the corresponding logs are mapped to a specific rule-file version so as to avoid failures and inconsistencies in the results.

The capture of the logs were driven by a push mechanism where the users had to submit the logs generated after running their experiments using Gush on PlanetLab. There is a standard rule-set that was designed based on the Gush semantics, but that could miss application-level fine-grained provenance. For that, scientists were allowed to enhance the standard rules to capture detailed information specific to their application. The tool, called the adaptor, would transform the raw log data into structured provenance events and store it in a database for visualization and analysis.

The complete framework including the utility tools are open source and accessible to scientists running experiments on PlanetLab. The default rule-files are packaged as part of the release along with a few enhanced rule-files specific to some experiments for fine-grained provenance capture. Sample logs were provided as part of the package to test and reproduce the results. The softwares and related documents are all open to public under the Apache license. Sample tests can be run using the wrapper scripts provided within the package. The software tools and related documents are available from http://d2i.indiana.edu/provenance_karma.

*(500-800 words)*

# Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them? (200-400 words)*

The major problem in reproducing the results was the frequently changing log semantics. This would frequently invalidate the default rules created for capturing provenance. So, the problem was maintaining the mapping between the dependencies and keeping the rule-files constant. The problem was addressed in two ways. In the first solution, every rule-file was associated to a version of Gush which generated the log. In the second solution, the rule-file itself contained a simple rule that could help identify and parse different versions of log files.

# Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

In order to make a reproducible workflow, I provided all the sample data and scripts that were used to generate the results. Specifically, I provided a standalone package for executing, correlating and visualizing the results and a benchmark to compare the results against. I also classified between the cases where the "reproducibility" of the workflow might fail.

# Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*



*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

## Why do you think that reproducibility in your domain is important?

I think reproducibility is important to both validate and reuse the research outcomes.

## How or where did you learn about reproducibility?

## What do you see as the major challenges to doing reproducible research in your domain, and do you have any suggestions?

In my opinion, there are a few technical challenges in reproducible research in the field of computer science. First, performance reproducibility is hard since it depends on a lot of random and unpredictable factors. Second, the amount of data required to reproduce the results may not always be known. Third, the extent to which a research can be reproduced might be hard to quantify due to several related but unpredictable dependency changes.

## What do you view as the major incentives for doing reproducible research?


Improved quality research due to trustworthy results that can be validated and reuse of data for future research.

## Are there any best practices that you'd recommend for researchers in your field?

## Would you recommend any specific resources for learning more about reproducibility?
