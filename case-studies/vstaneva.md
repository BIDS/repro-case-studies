##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*


1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.


My name is Valentina Staneva and I am an applied mathematician who develops methods to extract information from data (most of my experience has been working with image data). I am currently a data scientist at the eScience Institute at University of Washington. 

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

"Reproducibility" has two meanings for me:

(1) "Exactly reproducible" - when a result can be regenerated exactly as suggested given the same set of inputs and parameters. For example: a manuscript is "exactly reproducible" when one can provide some scripts and environment which with a press of a button (or an explicit set of instructions) can generate all the figures and calculations in the manuscript.

(2) "Approximately reproducible" - when a result or similar performance can be generated with similar or different methods than the one proposed on the same or possibly slightly different data. Often in science, the goal is to test a hypothesis and the methods to achieve this do not matter, it is actually better if the same hypothesis is supported through different approaches. Further, the data on which the study was performed might never be observed again, so it is not so important to reproduce the results on these data, but it is important to produce similar results on similar data. We are interested in the robustness of the methods and the conclusions, and a better term may be "robustly reproducible".


##### Workflow diagram



##### Workflow narrative:

I will describe the workflow of a project I did in grad school. It directly addresses the first type of reproducibility, but it explores also a bit of the second interpretation. 



This work follows more or less standard flow for problems in my field: motivated by an existing algorithm, we aimed to extend it to processing sequences of images (as opposed to a single image). Usually the process involves experimenting with different models of the data and different inference algorithms (intertwined with discussions with my advisor and literature reviews). The cross product of these models and algorithms can be tested on three main types of data sets:

- a data set simulated from the assumed model: since the data set is coming from the "correct model", this experiment is mainly testing the performance of the inference algorithms

- a data set simulated from a model which deviates from the assumed model (in some interpretable way): this  experiment is testing the robustness of the algorithms

- a 'real' data set: a video of a moving object; this tests the applicability of this methodology in practice

This results in exploring quite a lot of different setups and most of the research time is spent at this stage. The work was performed on an account on a university server, which was sequentially backed up. I also used Subversion for version control and stored my files in a Dropbox folder (which has its own version control). Luckily, I never lost a file, even when our server got hacked.

In general the evaluation of these algorithms on real data is difficult. There are no standard testing data sets: and it is hard to design ones as different image sequences describe different processes, and some algorithms perform well in some situations and poorly in other. One usually considers a range of typical tracking hurdles and checks whether a given algorithm can overcome them. Since there is no one final metric to submit this requires storing all the results from all the experiments. In the end I saved all the code, data, experiments and outputs in a folder, which one can use to regenerate the results (on Linux with Matlab: on Windows one would only need to change the slashes in the path directories). 

The workflow also contains a parallel path in which one studies the mathematical properties of the models and algorithms. The advantage of such an approach is that you can sometimes guarantee the performance (at least on simulated data) even without implementing the algorithms, which makes reproducibility of mathematical research quite easy!


##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*


1) Privacy: data issues - some of the motivation for this project was driven by the need to process a specific data set of cardiac data and do statistical analysis on the obtained results. I worked directly on processing this data set but during the process there was an a problem and I was advised not to use this data set (even though it was anonymized). I resorted to searching for a public cardiac data set which turned out extremely difficult: a website which aimed to maintain a public database of cardiac images was permanently down as the creator left the field. One good source for public biomedical datasets was MICCAI conference challenges: they contain datasets on which to assess methods for solving very specific problems, so sometimes the datasets were not complete. The data set I obtained for my testing did not contain ground truth relevant to my problem.

4) Volume: (Storage) since I worked with processing video sequences, an issue was simply arising from the size of the produced outputs;  If I generate many experiments: which should be done when dealing with MCMC simulation, I had to store many videos. Since I did not have a ground truth, I could not store just some small measure of mismatch instead of the whole sequence. Github's does not accept files larger than 100MB. This caused difficulty when trying to upload even only the input data to the repository. One of the images sequences was 600MB so it could not be uploaded. Waiting on Github to increase the limit to 1GB in the coming months. 

5) Randomness: working with Monte Carlo simulations results in different outputs every time the algorithms are applied. This requires the extra step of forcing the random number generators producing the same sequence of random numbers. This procedure is not so simple when parallelization is involved: MATLAB (and similar scripting languages) usually do not have control over the order in which the separate threads are started and that results in extra randomness in the output. One solution is to generate all random sequences that would be needed in the parallel threads in advance, but this requires modification of the programs themselves. Working with random outputs makes it hard to generate unit tests: we only have asymptotic results of what the outputs should be, so it is hard to set the confidence intervals for the outputs even with simulated data. 

6) Backup: I was using Subversion for version control of this project. I wanted to use the integration with the Nautilus file manager that Subversion was providing. It turned out it was buggy (it was a new feature) and not all commits and adds were recorded through the graphical interfaces: quite dangerous!



##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

I find two main reasons for the importance of reproducibility in my domain:

- personal: working with image data is often quite involved, and one does not want to do things twice, but it is often necessary, and in that case it is better to have an automated process to repeat experiments.

- public: there is overabundance of algorithms and studies but it is hard to use them in practice, because there is no simple way to reproduce the results (one usually needs to reimplement the algorithms or redo the studies) So if one wants their research to be useful outside their own group, they should first ensure it is reproducible.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I have learned by myself. I believe some short reproducibility workshops would have improved my experience substationally (for example, learning about git, virtual environments and light virtual containers). 

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

Working with biomedical data always causes privacy issues and storage issues. Another problem which I did not encounter but I know is persistent in the field is the use of too many external software packages to preprocess the data (some of them are supported only by specific Operating Systems). This makes hard to automate the workflow. 


4) What do you view as the major incentives for doing reproducible research?

I think the incentives should be personal and based on the understanding that this would improve the workflow and this is how research should be done. Unfortunately, the time and efforts spent on creating reproducible research are not very well awarded.

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

Be reproducible every day! It is much easier to perform reproducible research than making your research reproducible (after it was already performed).


6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

Some useful resources have been compiled by the eScience Reproducibility working group:
http://uwescience.github.io/reproducible/

Other resources:
https://github.com/Reproducible-Science-Curriculum

Coursera Class:
https://www.coursera.org/course/repdata









