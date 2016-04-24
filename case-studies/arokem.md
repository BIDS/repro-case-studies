# Reproducibility in human neuroimaging research : a practical example from the analysis of diffusion MRI.

##### Introduction

1) Who are you and what is your research field? Include your name, affiliation,
discipline, and the background or context of your overall research that is
necessary specifically to introduce your specific case study.

My name is Ariel Rokem. I am a Data Scientist at the University of Washington
eScience Institute. My research training and experience have been mostly in the
field of human cognitive neuroscience. During my postdoctoral training
(2011-2015) in Prof. Brian Wandell's group, at the Department of Psychology at
Stanford University, I conducted studies of human brain structure and function,
using quantitative MRI. A focus of the research program that I started in
Brian's lab is the application of ideas from statistical learning theory to
measurements of human white matter with diffusion MRI (dMRI).

2) Define what the term "reproducibility" means to you generally and/or in the
particular context of your case study.

Reproducibility is a matter of degree, not of kind. It usually depends on the
availability of code and data from a scientific study, such that only a
reasonable effort would be required to generate the evidence (numbers and
visuals) used to support a scientific finding.  

Ideally, a small number of commands at the command line would suffice, but in
some complex cases, more work could be required. A reasonable amount of effort
required might be rather extensive, when large amounts of data storage, or large
amounts of computation are needed.

A higher standard, sometimes called 'replicability' would be to require that the
same conclusions be reached if another group of researchers were to do the same
experiments, and implement the same ideas in their analysis.

Reproducibility does not guarantee replicability [Leek and Peng, 2015]. Some may
even argue that reproducibility and replicability may sometimes be in conflict,
because implementation errors can be propagated in reproduction, but not in
replication [Peng2009, Baggerly2005].

##### Workflow diagram

[Diagram](arokem_edited.pdf)

##### Workflow narrative

Measurements of dMRI are used as a way to assess the structure of the human
brain and its connectivity *in vivo*. Many parameters of the measurement are
determined by the experimenter, and incur trade-offs between sensitivity and
signal-to-noise ratio (SNR). Models of the white matter based on different
measurements are commonly used to make inferences about connectivity and tissue
properties, but there was no extensive study of the fits of these models to the
data, and no assessment of the effects of measurement parameters on the model
fits. In the study described here, we used cross-validation to evaluate two
commonly-used models in a variety of measurement conditions. The work was
published in [PLoS One](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0123272)

The project started with the collection of MRI data. Six participants were
scanned in different experimental conditions. The data were collected in the
Stanford Center for Neurobiological Imaging (CNI). The CNI has developed the
Neurobiological Image Management System [Wandell et al. 2015], which captures
the data from the scanner, archives it, and exposes a web interface that allows
researchers to control access to the data, and copy it into the lab's data
storage, a RAID (redundant array of independent disks) system.

The data were preprocessed using standard procedures (in the sense that any
practitioner of MRI would perform these steps on his or her data). This includes
correction of motion artifacts, alignment to a common coordinate frame, and
tissue type segmentation. These steps were performed once, at the beginning of
the study. The code that performs these steps is part of the lab code
distribution, [`vistasoft`](https://github.com/vistalab/vistasoft), freely
available through Github. Preprocessing also relied on freely available software
from other labs.

These preprocessed data are publicly available through the Stanford Libraries
Stanford Digital Repository (SDR), as two different collections:
http://purl.stanford.edu/ng782rw8378 and http://purl.stanford.edu/rt034xr8593.
Most of the data was licensed under the Creative Commons Atttribution license,
and a small subset was also released under the Public Domain Dedication License,
for unencumbered use in methods development.

Subsequent analysis was conducted on these preprocessed data, using a Python
library: [`osmosis`](https://github.com/vistalab/osmosis). This includes
implementations of methods for fitting the data, statistical analysis,
simulations and visualization, as well as utility functions  to handle parallel
execution on an HPC (high-performance computing) cluster. The library depends on
many components of the scipy stack, including `numpy`, `scipy`, `matplotlib`,
`scikit-learn`. In addition, the code depends on components of the [neuroimaging in Python](https://nipy.org) libraries. Approximately 30% of the module code was
covered by unit tests, with a particular emphasis on core modules and utility
functions that were reused. A few end-to-end tests were implemented to track
regressions. Development of the software was done openly on Github, and it was
also released under an attribution license.

Scripts using the module code were developed using the IPython notebook. These
scripts were run and edited many times, and as the project evolved a few of
these were copied into a [documentation folder](https://github.com/vistalab/osmosis/tree/master/doc/paper_figures), with
notebooks named "Figure1.ipynb", "Figure2.ipynb", etc, each corresponding to a
figure in the paper. In writing the paper, these figures were saved and
additionally manually edited by hand to add labels and annotation, and then
integrated into a Word document file, which was used to collaborate on writing
with the other authors. The writing process was not versioned throughout, but
several versions of the article were submitted to the arXiv preprint server,
while the article underwent peer review.

Most of the computations during the development of the project were conducted on
a lab multi-core compute server, that was running an IPython notebook server.
Thus, much of the development of the code was done on a laptop, over a web
browser, connected to the server. Some procedures described in the paper would
require an inordinate amount of time, without the access that we had to an HPC
cluster. For example, testing different settings of model regularization
parameters required fitting the models hundreds of times. Data was accesible to
the cluster through a mount of the lab RAID. Tasks run on the cluster were
managed through a queue system (Sun Grid Engine), and a module was developed
(`osmosis.parallel`) to facilitate submission of code to the cluster. These
scripts could not be used as IPython `ipynb` files, and were separately invoked
on the command line, but they are included as part of the code distribution,
recording these steps.

The IPython notebook documenting the steps that required parallel execution
includes both a 'precomputed' version (where parameters of the analysis are read
from precomputed files), and 'complete' versions, which include the code that
would have to be run to reproduce these results entirely on a single machine.
Precomputed parameter files were not made publicly available, and would have to
be recomputed to reproduce the results in these notebooks.

Though reproduction of the results in the paper could, in principle, be achieved
using this library, it is not neccesarily useful as a tool for others to work
with, and not easy to extend beyond the models that we tested. During the work
on this project, I became involved in an open-source project, which develops
Python software for the analysis of dMRI data: [Dipy](http://dipy.org). The main
ideas in `osmosis` were eventually ported into Dipy, accomodating the
application programming interfact (API), documentation and testing requirements
of that project. Furthermore, the prediction and cross-validation API
implemented in Dipy that I implemented in `Dipy` is designed to be sufficiently
general to accomodate new models, and mechanisms to evaluate their performance
in fitting dMRI data.

Through Dipy, the code in this project is now also distributed widely through
both Github and the Python Package Index (PYPI), under the permissive BSD
license.

##### Pain points

One of the main difficulties encountered was the duration of some of the
calculations. Some of the models, when fit on the entire brain volume, would
require many hours. In particular, using the IPython notebook as a computational
environment proved to be limiting, because connection to the kernel is only
reliably maintained as long as the computer running the browser is kept on and
prevented from sleeping. This also made it hard to perform computations that
required a long duration in the notebook. One of the ways to deal with this was
the development of caching mechanisms for model fit parameters. The models would
be fit using a script, and the paramters cached to file. The model instantiation
in the notebook would then know how to load these parameters from file, if the
file existed.

Another point of frustration was that as the code in the modules evolved, code
that was stored in the notebooks become outdated, and was no longer usable. This
meant that as the analysis code itself evolved, new notebooks had to be written.
Furthermore, as the writing and review of the article proceeded, figures were
moved around in the article, and other figures got added; Figures that had
started as appendices were integrated into the body of the article, etc. Thus,
it might have been better to wait until the end result was an accepted article,
and only then organize the entiree reproducible workflow that led to this
result.

##### Key benefits

Though sometimes cumbersome and effortful, one of the major benefits of the
process of producing a reproducible workflow is the level of confidence in the
results. There is never a doubt about what code is associated with what result,
because the full chain of evidence is documented in the code leading to that
result.

##### Key tools [Optional]

A specific module (`osmosis.parallel`) was developed to deal with submission of
jobs to parallel execution on the HPC cluster. This module would read in a
'template' script, and then create from this template, Python script files that
contained the instructions to run the fitting process with different conditions,
or on different parts of the same brain. The creation of this module resulted in
a highly reproducible process. Consequently reuse of elements of this module
produced benefits in time-saving during the development of the analysis methods.

##### General questions about reproducibility [Optional]

1) Why do you think that reproducibility in your domain is important?

Human neuroscience is a field which is particularly likely to have an abundance
of false findings [Ioannidis 2005]: Sample sizes are usually small, particularly
in MRI, which is an expensive experimental technique. The standards of the field
focus on statistical significance of effects, rather than effect sizes, which
tend to be small. Though standards limiting the selection of tested
relationships, and limiting the flexibility of experimental and analytic designs
are starting to emerge, in practice these are not very strictly limited. Some of
the aspects of the field that make it interesting and important, are also
pernicious in this regard: the direct application to human health means that
there is a perception of potential financial incentives. Finally, it is a
burgeoning field, with many groups working on similar questions. Higher
standards of reproducibility in this case would mean less false findings,
because at least some of these factors would be ameliorated by a full "chain of
evidence" to support every finding.

2) How or where did you learn the reproducible practices described in your case
study? Mentors, classes, workshops, etc.

Many of these practices evolved out of laziness. Early on in grad school, I
learned that most analyses that are done once, need to be redone, and that
ultimately I would have to do less work, not more, if I had a script that
generated all my figures for every study that I was doing. This also evolved
from being rather bad at taking notes about the work I was doing in the lab. I
would need programs, and eventually IPython notebooks, just to remember what I
did to get from the data to the conclusions.

A huge impact was the mentorship I got from Fernando Perez during graduate
school. He was not shy about how little of the research in our field he believed
to be true, and this skepticism inspired me to struggle to be more confident in
my own research conclusions.

3) What do you see as the major pitfalls to doing reproducible research in your
domain, and do you have any suggestions for working around these? Examples could
include legal, logistical, human, or technical challenges.

There are several barriers to wider adoption of reproducible research practices
in human neuroscience. The first is that there is very little practical cost to
not being reproducible. As mentioned above, there is likely to be a large
proportion of false results in the neuroscience literature, and it's more likely
to be false if it's not reproducible. Since a false positive result is more
likely to result in a publishable unit, there seem to be incentives in place to not be reproducible, slowing down the progress of the entire field.

4) What do you view as the major incentives for doing reproducible research?

The level of confidence that I have in my results is quite high. That helps me
sleep well at night.

5) Are there any broad reproducibility best practices that you'd recommend for
researchers in your field? + 6) Would you recommend any specific websites,
training courses, or books for learning more about reproducibility?

There are several papers that provide guidelines for reproducibility with a
specific focus on neuroimaging. Two recent examples include [Gorgolewski2016]
and [Pernet2015].


##### References

J.T. Leek and R.D. Peng (2015). Opinion: Reproducible research can still be
wrong: Adopting a prevention approach. PNAS 112: 1645-1646

B. A. Wandell, A. Rokem, L. M. Perry, G. Schaefer, R. F. Dougherty (2015). Data
management to support reproducible research. arXiv:1502.06900v1

A. Rokem, J. Yeatman, F. Pestilli, K.N. Kay, A. Mezer, S. van der Walt, B.A.
Wandell (2015). Evaluating the accuracy of diffusion MRI models in white matter.
PLoS One, DOI: 10.1371/journal.pone.0123272.

Ioannidis, J.P.A. (2005). Why Most Published Research Findings Are False. PLoS
Medicine 2: e124-

Roger D. Peng (2009) Reproducible research and *Biostatistics*. Biostat 10:
405-408

K. A. Baggerly, J. S. Morris, S. R. Edmonson and K. R. Coombes (2005). Signal in
Noise: Evaluating Reported Reproducibility of Serum Proteomic Tests for Ovarian
Cancer. J Natl Cancer Inst (2005) 97: 307-309.

K.J. Gorgoloewksi and R. Poldrack (2016) A practical guide for improving
transparency and reproducibility in neuroimaging research.
http://dx.doi.org/10.1101/039354

Pernet C and Poline, J. B. (2015). Improving functional magnetic resonance
imaging reproducibility. Gigascience 4: 15. DOI: 10.1186/s13742-015-0055-8
