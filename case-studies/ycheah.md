##### Introduction

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is You-Wei Cheah, and I am a computer systems engineer at Lawrence Berkeley National Laboratory. My background is in the research of computational data provenance. The workflow I am describing is the process, from idea inception to delivering a framework for managing data and metadata that allows the reproduction of scientific experiments in the Carbon Captures Simulation Initiative project.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.
In the context of my case study, reproducibility means that the decision process and the necessary data needed to reproduce a piece of software is sufficient to be executed by someone.

##### Workflow diagram
[Workflow-diagram](https://github.com/yocheah/repro-case-studies/blob/master/case-studies/ycheah.pdf)

##### Workflow narrative
This workflow describes the process to which the Carbon Capture Simulation Initiative (CCSI) Data Management Framework (DMF) was developed. CCSI is a large project that involves multiple national laboratories, academic institutions and industry partners to develop and deploy state-of-the-art computational modeling and simulation tools for accelerating commercialization of carbon capture technologies.

The workflow begins as a result of an ongoing need for a shared data repository for the CCSI project. A number of use cases have been gathered from the earlier years of the project. These use cases involve the need for integrating existing simulation and modeling tools from other CCSI teams to store both data and metadata of scientific experimental data. The DMF team starts of by analyzing these use cases and lists out the steps and goals needed to accomplish for each feature. Often times, the use cases need to be clarified and discussed with the external teams involved. Over time, the need for new features and integration are also proposed by different teams from the CCSI project.

Once solutions to these use cases are laid out, the DMF team moves to the prototype development stage. Prototypes are developed using both Python and Java and the code is stored in an SVN repository for version control. The prototypes are developed with sufficient capability so that they can be demoed and feedback may be solicited from users (in this case other CCSI teams). The prototype would then be demonstrated to see if the implemented features matched user expectations. Some back-and-forth discussion between the DMF team and the users will happen and this may require the DMF team to go back to the drawing board to reanalyze use cases.

If the features in the prototype match what was requested, the DMF team will proceed to further polish the prototype and prepare it for public release, this is also known as the production development stage. At this stage, extensive testing is done. Bug tracking and reporting is also done using JIRA, an issue tracking system. Jenkins, a build system is also used to automate the code build. If integration is required between external tools, this will be the next step. The integration step will go through the same intensive step with testing, bug-tracking and reporting. Again, the codebase is stored in the same SVN repository used during the earlier prototyping stage.

Finally, the DMF will be made ready for public release for our industry partners. This stage involves documentation of the existing code and writing of installation and user manuals using LaTeX. The codebase is also packaged alongside with documentation and finally released on the project website. The release is done perioridically throughout the year and once this is done, the process may be repeated when new features are requested.

The release of the DMF supports the storing of data and metadata in a shared repository and captures the data provenance of experiments done by scientists. Through the use of the DMF, users can track the necessary data involved used in different experiments. With this data, scientists can identify the actual data inputs that were used to generate scientific results and are hence able to reproduce results if necessary.

##### Pain points
The discussion of use cases and the design to address these use cases are not particularly well-documented. Some form of use cases and requirements exist in the form of tehnical reports. In general this is often done in an ad-hoc manner, and exists through communication of e-mails and discussions. In addition, the process of testing the Data Management Framework software is not particularly well-documented or reproducible. Some test cases and unit tests have been developed and placed into SVN to help with the automation of the test process. However, some of these cannot be easily tested, such as front-end graphical user-interface components. The code also has restrictions in the audience that it can be shared.

Since this is ongoing work, we are working on encouraging the use of JIRA as part of keeping track of feature requests and use cases. The use of test procedures are also developed to keep track of the procedures needed to test and to build a full test-suite to help keep track of potential issues.

##### Key benefits
Despite the shortcomings discussed above, a large number of code, documentation and bug-tracking have computing infrastructure setup and managed so that versions and decisions made are logged. The use of JIRA has generally made tracking and reproducibility of bugs and errors easiers. Users and testers are required to file bug reports. Code building automation using Jenkins is also done in a large extent such that code is build periodically to identify if faults are present and the integrity of code is maintained after a code commit or when integrating with other CCSI tools. The automation requires a higher amount of time initially for configuration and setup, but once done, this reduces the amount of overhead required to keep track of errors in the code base. The practice of using automated tools has been encouraged and is setup across the board for most of the CCSI tools so that integration is a breeze.
