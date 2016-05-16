---
title: Detection and Classification of Cervical Cells
running: Detection of Cervical Cells
author: Daniela Ushizima
---

My name is Daniela Ushizima, and much of my research work is in devising machine vision and pattern recognition algorithms as part of software tools for handling image-centric data, especially those arising from the Department of Energy imaging facilities. I am currently a [Staff Scientist](http://vis.lbl.gov/~daniela) at the Lawrence Berkeley National Laboratory and a [Data Science Fellow](https://bids.berkeley.edu/people/daniela-ushizima) for the Berkeley Institute for Data Science at the University of California, Berkeley. The case study I describe here illustrates the core steps in designing a machine vision algorithm to analyze a set of digital images and organize them according to the desired criteria. There are several image processing and analysis frameworks that encapsulate algorithms; this case study refers to [ImageJ](https://imagej.nih.gov/ij/), a powerful image analysis tool.

# Workflow

![Diagram](dushizima.pdf){width=100%}\

The workflow diagram follows a data model called SIPOC, which stands for suppliers, inputs, process, outputs, and customers; these correspond to the columns of the table. Here, we adapt SIPOC diagram to better represent our use-case, hence the first column is called sources and the final column represents repositories. The proposed workflow prioritizes the compartmentalization of different processing steps of the analysis system, and hides potential feedback loops that might occur.

This diagram tells the story of research investigations among doctors, pathologists, cytologists, and computer scientists, aiming to design, develop and deploy algorithms for improving the analysis of biomedical images. Some of the tasks include increasing the number of fields under scrutiny, speed up cell counting and recognition, comparison among cells, quantitative description of samples, to name a few.

Historically, this use-case begun with brainstorming among pathologists, physicist and software engineers on how to provide scalable computer-aided analysis to the available large datasets of digital images, containing [cervical cells](http://www.cancer.gov/types/cervical/understanding-cervical-changes/understanding-cervical-changes.pdf). Communication and diagraming were fundamental *sources* of information to understand how to well characterize types of cells and foresee limitations imposed by the datasets, such as cervical cell lineages, cell fragments, magnification and usable area within sample.

In order to develop analysis pathways, the team organized the datasets into three main *input* image sets: simulated, real and curated. A simulated image consists of several clipped real cells collated with different levels of overlapping, which facilitates algorithmic validation since the ground-truth is known a priori. A real image consists in a digital picture of a Pap smear slide, obtained at the light microscope -- these images often contain several types of cervical cells and others (e.g. bacteria, blood), and may be corrupted by noise and other artifacts, such as staining variations, dirt, etc.

The core of this case study lies in the *process* column that illustrates the main steps for the image analysis. The preprocessing step transforms the samples into more reliable representations of the image, for example, removing areas or eliminating the whole image if it is over-stained. This step includes essential image transformations, such as anisotropic filtering that preserves borders and smooths regions that are mostly homogeneous.

As part of the process, the software tool must detect the regions of the interest in each image, i.e., the cellular mass, as opposed to background. This step took a long time to evolve into an algorithm that could correctly split the image into foreground and the rest of the image. The next step is to separate the cellular mass into individual cells: by modeling simple biological prior knowledge, such as the relationship between nucleus and cytoplasm, the algorithm is able to quickly estimate cytoplasm boundaries. After identification of the cells, feature extraction takes place, including nucleus-cytoplasm area ratio, convexity of cytoplasm contour, and other parameters that are relevant on identifying cell lineages. Finally, we use simulated and curated datasets to validate results, for example, considering sensitivity and specificity measures based on the number of pixels or the number of cells identified.

An important step of the data processing is keeping track of the *outputs*. The forth column lists four main outputs of the system: technical reports, scientific papers, documentation about the software tool and educational material about the science problem and algorithm developments. Although the diagram omits output of partial results, they are very common and useful  throughout the design of the analytic software tools.

The fifth column shows the main ways in which *consumers* of the outputs will have access to the research discoveries, for example [Github](https://github.com/dani-lbnl/CRIC) and [websites](https://sites.google.com/site/cervicalcancercell/). In the context of this case study, it indicates the main hubs of information distribution for the project.

# Pain points

The software tool design and testing require intense communication among the team members through reports and presentations. Although part of team used version control, much of the code is still to be made available open-source through Github. In addition to commit messages, which tend to be short, we have also maintained technical reports, developed as a diary of activities -- these are fundamental to keep the whole team synchronized and up to speed. The painful side of diary or electronic lab books is mostly the free form of inputs that may require extra-time to parse.

# Key benefits

The most reproducible part of this project has been the development of code allied to simulated datasets. This activity improved across the team, particularly due to participation in code competitions organized by our consortium, which forced the whole team to organize data sources and code with eyes on easy re-run by reviewers. Keeping track of advancements in a common digital lab book helped considerably in preparing manuscripts and other technical reports.

# Key tools

An important tool has been ImageJ, a Java-based image processing software program, which was originally developed by Wayne Rasband within NIH circa 1997. Although most of the ImageJ plug-ins focus on medical imaging, this framework has been widely used in other applications, such as material sciences.

# Questions

## What does "reproducibility" mean to you?

In the context of this case study, the work will be computationally reproducible when the software tools our team builds can also be used by the science domain experts -- these must be able to transform raw data files into quantifiable patterns, obtaining consistent results with previous/tested analyses. Because algorithmic parameters often change from a dataset to another, it can be challenging to get results with the same accuracy, given different datasets.

## Why do you think that reproducibility in your domain is important?

Reproducibility is essential in quantitative microscopic because it is often associated to measurements and quality control.

## How or where did you learn about reproducibility?

Much of what I knew I needed to learn on my own, then I met Software Carpentry members and BIDS fellows. Lots of concepts came together more systematically particularly after attending Software Carpentry classes and becoming a instructor myself.

## What do you see as the major challenges to doing reproducible research in your domain, and do you have any suggestions?

The major pitfalls to doing reproducible research in image analysis are (a) the use of very simple examples to illustrate applicability of the algorithms, (b) dependency of packages that are not freely available, and (c) absence of documentation that enables understanding how/why the data transformations occur.

## What do you view as the major incentives for doing reproducible research?

The major incentives for doing reproducible research are the ability to replicate the experiments later, to fix and/or reuse code for different applications, to easily work in larger teams, and the potential for broader impact in the area.

## Are there any best practices that you'd recommend for researchers in your field?

While there are no general rules, some tools can only help one to reproduce work: (a) use version control, (b) practice [software quality assurance](https://en.wikipedia.org/wiki/Software_quality_assurance), (c) keep data samples.

## Would you recommend any specific resources for learning more about reproducibility?

Among the several options out there, [Software Carpentry](software-carpentry.org) is certainly one of the best resources and the book [Making Software](http://deca.cuc.edu.cn/Community/cfs-filesystemfile.ashx/__key/CommunityServer.Components.PostAttachments/00.00.00.22.46/Oreilly.Making.Software.Oct.2010.pdf) by A. Oram and G. Wilson.
