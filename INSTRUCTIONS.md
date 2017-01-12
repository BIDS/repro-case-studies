# Reproducibility Case Study

Thank you for volunteering to contribute to our reproducibility case study project. This document contains the following sections:

- [Project goal](#project-goal)
- [What is a case study?](#what-is-a-case-study)
- [Case study instructions](#case-study-instructions)
- [How to submit your case study](#submitting-your-case-study)

## Project goal

The overall goal of this project is to better understand and communicate existing practices surrounding reproducibility in academic research. Our strategy is to gather a collection of several dozen case studies, authored by individual researchers from across disciplines who volunteer to share their practices. Each case study will provide a single, concrete example of a workflow pipeline that embodies the principles of reproducible research. We do not intend to create another anecdotally-derived list of best practices or a discussion of the _why_ of reproducibility, but rather to gather and share examples of the _how_ of reproducibility practices in academia.

<!-- A case study takes the form of a ~1,500-2,000 word response to a series of short answer quetsions and a flowchart-style diagram, both described in detail below. The initial group of authors reported that a case study took approximately 2-4 hours to prepare. -->

As you prepare your case study, consider your audience to be advanced undergraduates, graduate students, and other disciplinary scientists who want to learn the "how" of reproducible research by example. We will work to publish these case studies as an edited volume, where you will be credited as a chapter author for your case study, and in a Github repo or other similar open online platform.

For more information about the project goals or framework, contact Justin Kitzes (jkitzes@berkeley.edu)

## What is a case study?

A case study describes the computational workflow that you used to complete a single well-defined research output (e.g., a manuscript or equivalent). A case study specifically should not describe a lab, a person, a concept, or a general hardware/software stack. It should be an example of a concrete research activity, not a reflection. The goal is to capture your web of practices surrounding a specific research pipeline and its associated benefits and challenges.

Broadly, there are two levels of case studies that are appropriate for submission. The first is a "high level" case study that describes all three major steps of a research pipeline, including data collection, data cleaning, and data analysis. The second is a "low level" case study that focuses in on one or two of these stpes in more detail. Examples of a [high-level case study](case-studies/jkitzes.md) and a [low-level case study](case-studies/dturek.md) are included in this repository for your reference.

When choosing a subject for your case study, __think small and concrete__. For a sense of scale, a case study should cover research representing approximately 6 months to 1 year of work for a single researcher. If your projects tend to be large or complex, you may choose to focus on only a portion of a larger project for your case study. If you do not have a single project that you feel would be useful to share, you can describe an "idealized" workflow that combines features of several different real projects, although we are particularly interested in hearing about projects that were partially successful or that involved significant difficulties.

## Case Study Instructions

The case studies should be written using Markdown. To help you complete your case study, we have provided a template that will guide you through a series of standard short answer questions. To complete your case study, simply open [this template](https://raw.githubusercontent.com/BIDS/repro-case-studies/master/template.md), save a copy of the template with a file name consisting of your first initial and last name (e.g. ``alovelace.md``), and replace all of the instructions with your responses. Length suggestions are provided for each section. You may also wish to refer to the two sample case studies ([high-level](case-studies/jkitzes.md) and [low-level](case-studies/dturek.md)) for guidance.

In summary, the core of the case study is a visual diagram showing your workflow with an accompanying narrative description. You'll also be asked for additional detail on specific pain points (portions of the reproducible workflow that were failed, incomplete, or particularly challenging), key achievements, and key tools. Several general questions on your views of reproducibility will complete the case study.  

Each case study will be short, with a target of ~1500-2000 words (~6-9 pages) for the final version. We encourage you to write more than this if needed in your initial submission, recognizing that the editors will later help you to to reduce this total.  

## Submitting your case study

If possible, please submit your case study as a pull request to this repository, as described in the instructions below. Alternatively, you may email your contribution, consisting of the completed template file and a workflow diagram, to Justin Kitzes (jkitzes@berkeley.edu). Please feel free to contact Justin with any questions on submission, the case study, or the larger project.

Here are the steps to submit a case study as a pull request:

- [Fork](https://help.github.com/articles/fork-a-repo/) the
  [repro-case-studies](https://github.com/BIDS/repro-case-studies)
  repository on GitHub.

- Clone that repository onto your local machine using git. 

- Two examples are provided in the `case-studies` directory. These are at `case-studies/jkitzes.md` and `case-studies/dturek.md`. Associated workflow diagrams are in the corresponding pdf files.

- Copy the `template.md` file into the `case-studies` directory, and name this file with your first initial and last name (e.g. `alovelace.md`) 

- Open the file and respond to each question. Experience has shown that it is easiest to answer the questions in the order presented.

- Add an image file(s) containing your workflow diagram as instructed in the template.

- Please do not modify any files other than your case study.

- Once you are ready to submit your case study, file a [pull request](https://help.github.com/articles/using-pull-requests/) on GitHub.
