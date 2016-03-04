**Beth Reid**  
**Reproducibility Case Study**  
**Alpha Stage**  

##### BACKGROUND
1) Who are you and what is your research field? Include your name, affiliation, discipline, and the context of your research program necessary to frame your case study.

Beth Reid, Berkeley Center for Cosmological Physics.

Cosmologists are systematically making maps of the universe.  These maps contain information about both the initial conditions of the universe, which we think were determined by physics operating at energy scales much higher than accessible on Earth, and the dynamics of the universe, which we think are dominated by gravity.  Two recent examples of such maps are the [exquisite measurements](http://www.esa.int/Our_Activities/Space_Science/Planck) of the cosmic microwave background by the Planck satellite, and the [three-dimensional maps](https://www.youtube.com/watch?v=08LBltePDZw#t=13) of the galaxy distribution over the latter half of the history of universe provided by the Sloan Digital Sky Survey telescope.  In this project I focus on the process of making these maps reproducible by other scientists.

The information of interest in these maps is statistical in nature: we are uninterested in the specific value of the temperature in a particular point in the sky.  Rather, cosmological information is encoded in the structure of correlations in the maps.  It is therefore imperative to correct for or at least characterize artefacts in the maps from the way in which the maps were constructed.  For instance, certain properties of the observational strategy ("fiber collisions") make correlations in the maps unreliable below the minimum separation of the spectroscopic fibers.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

In the context of this problem, it has a rather concrete definition: given the (version-controlled) input data files, an outsider should be able to compile and run our code (and its dependencies) and generate the same output catalog files that we are publicly providing.  As we will see, this could be quite an arduous task for someone working outside the SDSS environment, and frankly, we do not expect there to be a large demand for this ability.  So we shall consider a more modest goal for now, which satisfies the needs of most outside researchers as well as the the most pressing needs of the SDSS collaboration.  At the end we will consider what aspects of our workflow led to the resulting difficulty in reproducibility.  The level of reproducibility currently in reach is
  * Provide public copies of the catalogs used for the SDSS team analysis.
  * Provide a public copy of our code (i.e., our *algorithms* are public) and documentation of dependencies.

3) Why do you think that reproducibility in your domain is important?

Cosmology has (for the moment) converged on a standard model that heavily relies on the results of a few key experiments, again the CMB and galaxy maps being prime examples.  Many researchers outside the science collaborations have added extremely useful insights regarding the construction and analysis of those maps.  [One example](http://arxiv.org/abs/1003.0198) that immediately comes to mind is the discovery of a $9\sigma$ artefact from beam asymmetry in CMB data from WMAP, discovered as part of the Ph.D. work of Duncan Hanson.  Such improvements would not be possible without the concerted effort of science teams to make low-level data products (like time streams rather than only derived maps) available; see the [WMAP data products](http://lambda.gsfc.nasa.gov/product/map/current/) for an example.  However, CMB experiments do not generally release their analysis code for inspection, but do provide likelihood analysis codes that operate on reduced data products.

The SDSS collaboration developed significant infrastructure for external users to access SDSS data (one example is [CasJobs](http://skyserver.sdss.org/CasJobs/)) as well as making [some of the analysis code public](http://www.sdss3.org/dr8/software/products.php).

** BR: definitely need to fact-check many of the above statements in detail, but I think the spirit is correct.  Ask Martin White/David Schlegel for input here. **


4) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I have worked on both theoretical and observational/data analysis projects in cosmology, and all of my knowledge of reproducible practices comes from my work with observational projects.  I was introduced to how to use a version control system and some very basic software engineering practices during my Ph.D. when I was contributing to a common data analysis pipeline for the (Atacama Cosmology Telescope)[http://www.princeton.edu/act/].

In my work with the SDSS collaboration, I became familiar with the use software (and data product) tags; this was exemplified by the team of scientists/developers working on producing concrete and deliverable data products (like the list of targets to be observed by the telescope), but these practices did not trickle down into my science working group (I am at least trying to retroactively generate static copied of our software to reproduce earlier data releases). 

In my theory projects, I found that use of non-public, single author analysis code is the norm.  However, there are several examples of widely used theory codes (e.g., [camb](http://camb.info/) and [cosmomc](http://cosmologist.info/cosmomc/)).

5) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

Time commitments, often working to meet deadlines ("we'll clean up the code later") and lack of incentive. 

6) What do you view as the major incentives for doing reproducible research?

For the examples I discussed above, the incentive for the community (in terms of improving the robustness and scientific impact of data sets) to provide access to large and broadly interesting data sets is very high.  Public theory codes that provide solutions to problems of broad interest have also been demonstrably beneficial to scientists' visibility.  However, the incentive to complete the extra work to make an individual publication reproducible is not currently there. 

##### WORKFLOW NARRATIVE
*Workflow narrative and diagram - a textual narrative describing your workflow with an accompanying diagram showing your workflow visually*

This case study describes my work within a relatively large scientific collaboration, first as a contributor to a software product "mksample", and eventually as the primary developer and person responsible for producing and releasing data products from that code.

This collaboration is sufficiently large and software intensive that the project (at least partially) supports several scientists committed to specific software and data deliverables outlined as supported by the project; in our case these are reduced images (from which BOSS targets are derived) and spectroscopic reductions (in their simplest form for our purposes, galaxy redshifts).  It is the task of the science working group to combine these results into a large scale structure catalog.  The purpose of this catalog is to provide a best estimate of the galaxy fluctuation field at any point observed in the survey.  This requires keeping careful track of the efficiency of the survey as a function of position on the sky (the survey geometry/mask), and accounting for a series of observational artefacts.

My work, especially interactions with the software-focused project scientists, introduced me to several essential tools for reproducible and collaborative science:
 * Version control for software products.  There is a single svn repo available to the collaboration where new projects can be created.  The state of software in the "General" category is strictly tagged with data releases (and also at important changes to the code) so that each data product is reproducible, yet the code can continue to be developed.  Those working on BOSS science products in the galaxy clustering working group were unlikely to use tags properly (but rather kept versions informally, e.g. by putting dates in file names).
 * A version manager for tracking product dependencies.  We use [EUPS](https://github.com/RobertLuptonTheGood/eups/) to tailor each user's combination of software products and versions thereof.  As a developer within the science working group, I was unaware of how to use this product and for the most part did not need the functionality.  The EUPS product is set up on SDSS data processing/hosting machines but not generally used by the average science member of the collaboration.  The "mksample" code relies on hard-coding of which version of imaging data was used in which region of the sky.  In a perfect world, a single version would have been used for the entire survey; however, this is not a perfect world and the imaging reduction software was still being improved after the BOSS spectroscopic program began taking data. 

The difficulty in making the "mksample" catalog reproducible was that as the science teams' work progressed, we introduced dependencies on data and software products.  The normal mode of operation in the science team was individual groups developing analysis at their institutions and not sharing code on SVN.  Many competing projects doing essentially the same task (rather than trying to build a single, best product).  This may not be surprising, as often many approaches are pursued to solve the same problem if the solution is not obvious.  However, at least some of the motivation here is each scientist needs to generate his own novel scientific results, and sharing code can be a way of aiding the enemy. 

##### PAIN POINTS
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*

 * Building in dependencies to other libraries makes your code harder to sustain.  The version of pydl I was previously using was no longer being maintained (it was incorporated into astropy).  I spent a frustrating day or two diagnosing errors with the new version, which was not backwards compatible.  I was unable to get the project software scientist to install one of my dependencies on NERSC, so the code is not fully functional there.  In fact, managing dependencies on NERSC also looks potentially complex (e.g., the existence of [hpcports](https://theodorekisner.com/software/hpcports/).  My lesson learned is to avoid dependencies where possible (especially for newer or less used products), and use available tools to track them. 
 * Another pain point is to get scientists to contribute their own code (rather than an untracked data product).  The only solution I've found for this problem is to offer help in integrating the code, and it still only works occasionally.  Instead, scientists are often motivated to "own" their software products so they can get all the mileage out of them (rather than competitors).  There is generally a disconnect between software people (with very good code and data hygiene but rare to lead first author papers) and scientists (bad reproducibility hygiene, but good at finishing papers and producing results).
 * The mksample code evolved significantly as the goals of the working group and our understanding of the relevant physical effects evolved; this means that the final structure was significantly less clean, well-organized, and user-friendly that I had originally hoped. 

##### KEY BENEFITS
*An in depth discussion of ideally one, or possibly a few, sections of your workflow that you are particularly proud of and feel are particularly important or useful to others*

 * These LSS catalogs will be the premier dataset for years to come, and documenting how we produced them for future users with unanticipated applications is good for the benefit of science and also extends the reach of the project.
 * While I don't feel that software and computing tools are my strong suits as a scientist, I have learned a tremendous amount by getting deeply involved in a project and it will serve me well in my future endeavors.


##### TOOLBOX [OPTIONAL]
*If applicable, a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general*

 * SVN (for both code and paper writing).
 * collaboration wiki
 * EUPS (WOULD be useful if scientists used it)

