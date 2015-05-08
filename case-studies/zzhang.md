##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Zhao Zhang, and my area of research is computer science with a concentration on apply computer systems to support scientific applications. The workflow I describe is the process of building Kira, a distributed astronomy image processing pipeline in the cloud environment. We use the SEP library for domain computation, Apache Spark for task coordination and I/O, Apache HDFS for persistent storage.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In the context of my case study, reproducibility has several levels of meanings. The very baseline is that users can compile the source code and pass the tests. Secondly, users should be able to configure the computer cluster so the can repeat the performance in the documents. Since it is impossible for them to repeat the exact number for every single run, a statistical repeat should be fine (average performance with bounded variation). Generally for computer system research that involves data, a public availale data source is necessary for the performance to be reproducible.

##### Workflow diagram

[Diagram](zzhang.pdf)

* specialized tools and where they enter your workflow
We use Latex and Slides to track the merit evaluation: why do we need a new system for astronomy image processing, what makes it a better system, what lessons can we learn from this research.

We use Latex and Github repository to keep the system design, it is basically a diagram.

We use a private Github repository to keep track of solutions for technical barriers such as I/O processing, Spark interaction with C program, Spark system parameter configurations and many others.

The whole system is built with multiple programming languages and tools. At the programming language level, we use Scala, Java, and C. At the system level, we use Spark for task coordination, HDFS for persistent storage, SEP library for actual computation.

The source code of the project is kept in a public Github repository for open source purpose. 

The manuscript is being kept in a private Github repository since it is under review.

* the "state" of the data at each stage
In system design phase, we decided to use three datasets four development, testing and performance measurements. But we end up with four datasets.
A trivial dataset that contains only a few image files is used for development and testing.
A small dataset (12GB) is used for quick verification at scales.
A large dataset (65GB) is used for large scale performance measurement.
A fourth dataset (1TB) is used to show the data processing capacity of the Kira system as we put up the paper.

All these datasets come from the Sloan Digital Sky Survey. Some of them are from Data Release 2 while some are from Data Release 7. We choose them arbitrarily as we care more about the system capacity rather than the science in this research.

* collaborators
Kyle Barbary, Oliver Zahn, Saul Perlmutter are astronomers.
Frank Nothaft, Evan Sparks, Michael Franklin, David Patterson are experts about Spark and cloud computing in general.
Zhao Zhang has rich experience in HPC community and some experience in cloud computing as well as a bit astronomy background.


* version control repos
We use private Github repository for manuscript management and public Github repository for project management.


* products produced at various stages (graphics, summaries, etc)
We have summaries for Team Brainstorming and Merit Evaluation phase. 
System Design's output is in the form of figures and is kept in Github repository.
Solutions for Technical Barriers are kept in a private Github repository.
Documents, Source code, system configurations as the products of coding/testing/tuning/measurements are kept in a public Github repository.
The paper draft is kept in a private Github repository.

* databases

* whitepapers

* customers (if any)

##### Workflow narrative

The process begins with team brainstorming of how modern computer software and hardware can accelerate the astronomy image processing pipeline. This requires a wide and also deep understanding of the state-of-the-art research and technical solution. In this research, we gather domain expertise (astronomers), cloud computing expertise and high performance computing expertise. We review the existing work and we think using cloud computing software-hardware stack can improve the overall application performance, but we have no idea how much it can improve. The research is an exploratory process to implement the idea and quantitatively measure the improvements if there is any.

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

[Answer, 500-800 words]

##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*

I will break this down to reproducible results and reproducible research progress.

1. (reproducible results) For the results to be reproducible, the readers should be able to tell and access the computers with the same hardware, the code base used particularly for the experiments, the dataset that was used for performance measurements. 

1.1 Hardware access. Since we are using Amazon EC2 resources, the same computer hardware is mostly accessible unless Amazon upgrades the hardware. It happens every few years. A second risk is that for large scale test, the reader might contact Amazon to increase the hardware limit which Amazon uses to limit the quantity of resources each user can posses at the same time.

1.2 Code base. We maintain our code under a public Github repository, so it is accessible to all. However, the pain point is that the software evolves and the performance might change with the software evolution. Thus it is important that the authors should let the readers know which version of the software is related to the results that readers care about.

1.3 Dataset. The astronomy image dataset we use is Sloan Digital Sky Survey Data Release 7, which is publicly accessible. As long as the data hosting service is up running, the dataset is available. We also make a copy of the dataset we used in Amazon S3 service with public accessible permission. The pain point is that we have to pay Amazon for maintaining the 1TB dataset, and eventually we will run out of funding, so instead we have to publish the dataset file list as a text file in the code base.

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example?*

I break this question down to two: non-usable workflow and non-reproducible workflow.
1, Non-usable workflow. I have seen a couple of projects in astronomy, where the authors conducted study on applying new tools to solve the old problems, but the authors failed to publish their source code along with the paper. This gives up the opportunity for people to build solutions upon their work. For Kira, we make the source code available on Github, so people can extend this code base for more functionalities.

2. Non-reproducible workflow. There was one experiment I read in a paper that I would like to reproduce, and design a new solution for it. However, the experiment was not reproducible due to the software version evolution. During the Kira building process, we particularly care about this issue, we documented the hardware, code base and dataset that are used for the performance measurement, so any user that follow the documented instructions should be able to reproduce the results.


##### Key tools [Optional]
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience.*

Github for code management, and Amazon S3 service for data hosting. We built Kira with Apache Spark which is a highly active open source project, so that we do not have the concern of the computing framework is out of maintenance if they run out of funding in academia. 

##### General questions about reproducibility [Optional]

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

As computer system researchers, we build systems assuming people will use them. So it is important that people can follow the instructions in the documents to reproduce the state in which the system works. And it is important that users can reproduce the improvements over existing systems we describe in the paper or documents so they are more likely to adopt our systems. As paper reviewers, it is more convincing if they can reproduce the results in the paper as these are the evidence of the paper's idea.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I learned the reproducible practices since the first time I submitted my homework project in college and ever since. I need to write a README file along with my code so the TA can compile and run my code to test if my solution is right. The later research experience follows the same path. 

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

I used to design systems on supercomputers, where many people including paper reviewers have no access to. Thus, it is impossible for the research to be reproducible. 

Another major pitfall is due to software version evolving. At the time of writing the paper, some features of a piece of software was working, and the researchers measured and published the numbers. But these numbers are no longer reproducible after a few versions.

4) What do you view as the major incentives for doing reproducible research?
I break this down to reproducible results and reproducible research process.

4.1. (reproducible results) The systems I build are usually to facilitate scientific research. The systems either expedite the execution of computer programs or provide novel functionalities (e.g. failure diagnosis). To make sense about my research, users should be able to see the performance improvement I documented in the paper or documents. They should be able to use the novel functionalities to ease their research. So reproducibility of the systems is the key to prove the system actually works.

4.2. (reproducible research process) As a whole process, this particular research case is exploratory. We only have a conjecture about the performance before the implementation and measurement. I am not familiar with the tools I am using also (Apache Spark, Scala, Java Native Library, SEP library, Source Extractor C program). I think (not quite sure) the incentive for the reproducible research progress is helpful in my future projects. Once again, if I am facing such situation, I know where to start to tackle a complicated problem.
My methodology particularly for this research is: 1) a more-or-less valid hypothesis, 2) a performance profile of the existing solution, 3) isolating the technical barriers, 4) solving the technical barriers, 5) build the new solution, 6) performance measurement and tuning. 


5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

I would recommend for open source software and related publications. The authors should maintain a version of the software for readers to reproduce the results in the paper. These versions and repository should be included in the paper.

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

I can only think of Github for code management and Amazon S3 for data management right now.
