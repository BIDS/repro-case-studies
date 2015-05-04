##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Zhao Zhang, and my area of research is computer science with a concentration on apply computer systems to support scientific applications. The workflow I describe is the process of building Kira, a distributed astronomy image processing pipeline in the cloud environment. We use the SEP library for domain computation, Apache Spark for task coordination and I/O, Apache HDFS for persistent storage.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In the context of my case study, reproducibility has several levels of meanings. The very baseline is that users can compile the source code and pass the tests. Secondly, users should be able to configure the computer cluster so the can repeat the performance in the documents. Since it is impossible for them to repeat the exact number for every single run, a statistical repeat should be fine (average performance with bounded variation). Generally for computer system research that involves data, a public availale data source is necessary for the perfomrnace to be reproducible.

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

All these datasets come from the Sloan Digital Sky Survey. Some of them are from Data Release 2 while some are from Data Release 7. We choose them arbitrily as we care more about the system capacity rather than the science in this research.

* collaborators
Kyle Barbary, Oliver Zahn, Saul Perlmutter are astronomers.
Frank Nothaft, Evan Sparks, Michael Franklin, David Patterson are experts about Spark and cloud computing in general.
Zhao Zhang has rich experience in HPC community and some experience in cloud computing as well as a bit astronomy background.


* version control repos
We use private Github repository for manuscript management and public Github repository for project management.


* products produced at various stages (graphics, summaries, etc)
We have summaries for Team Brainstorming and Merit Evaluation phase. 
System Design's output is in the form of figures and is kept in Github repository.
Solutions for Technical Barriers are kept in a private Github reposirty.
Documents, Source code, system configurations as the products of coding/testing/tuning/measurements are kept in a public Github repository.
The paper draft is kept in a private Github repository.

* databases

* whitepapers

* customers (if any)

##### Workflow narrative

The process begins with team branstorming of how mordern computer software and hardware can accelerate the astronomy image processing pipeline. This requires a wide and also deep understanding of the state-of-the-art research and technical solution. In this research, we gather domain expertise (astronomers), cloud computing expertise and high performance computing expertise. We review the existing work and we think using cloud computing software-hardware stack can improve the overall application performance, but we have no idea how much it can improve. The research is an exploratory process to implement the idea and quatitatively measure the improvements if there is any.

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

[Answer, 200-400 words]

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example?*

[Answer, 200-400 words]

##### Key tools [Optional]
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience.*

[Answer, 200-400 words]

##### General questions about reproducibility [Optional]

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

[Answer]

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

[Answer]

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

[Answer]

4) What do you view as the major incentives for doing reproducible research?

[Answer]

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

[Answer]

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

[Answer]
