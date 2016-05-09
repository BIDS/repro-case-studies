##### Title

pyMooney: Generating a database of two-tone, Mooney images 

##### Introduction

I am Fatma Imamoglu a postdoctoral fellow at the International Computer Science Institute, Helen Wills Neuroscience Institute and a Data Science fellow at Berkeley Institute for Data Science. 

I work on computational neuroscience. The current case study will only describe one part of my usual research pipeline, i.e., stimulus generation. Every successful neuroscience experiment needs to run several pilot experiments to create the best stimulus that is suitable for one or several questions that the researcher is asking for. Hence, this step is usually tedious, where different parameters are tested until a final set of stimulus is used in the experiment. In order to build upon the work a researcher has already conducted or to create new experiments (with new hypothesis) using the same stimulus set, it is very important to have access to the stimulus that has been used, or to create new stimulus with the same parameters or algorithmic procedure.

In this case study I will focus on a image database that was created for a specific cognitive neuroscience question. After the experiment was published the database has already been used in several other experiments. The images that I created for the study were two-tone, Mooney images. These images are binary, black and white images, where a single hidden object is only recognizable when the original image has been shown previously to the observer, the hidden object was outlined, or after a certain time when the observer finds hints in the image that follows with recognition. These different steps of recognition makes such stimulus creation very difficult. Using these images in the original experiment (Imamoglu et al. 2013) I asked whether functional connectivity in the human brain is altered when the hidden object is recognized vs. when it is not recognized.

##### Workflow diagram

[Diagram](fatmai.png)

##### Workflow narrative

Generating two-tone, Mooney images start with a selection of concrete words. There is a database called [MRC Psycholinguistic Database](http://websites.psychology.uwa.edu.au/school/MRCDatabase/uwa_mrc.htm) where each word has been labeled as concrete or abstract, how frequently it is used, etc. From this database I selected 967 concrete words. The necessary parameters are saved in a config file (e.g. concreteness rating and imageability rating between 550 and 700). These concrete words are saved in a CSV file. Based on these words I downloaded real-world
images tagged with these concrete words from an online image database (Flickr) in an automated fashion using custom written **pyMooney** python package. This package is based on a python API (Flickr API) and the scikit-image library. Each project needs to have a config file that specifies e.g. whether the Mooney images are created based on images that are stored locally or whether the images should first be downloaded from the image database. If images are downloaded from an online resource licensing information needs to be set in the same config file. Using a smoothing and thresholding process (Otsu, 1979) and prescreening of images, I created a database of 330 two-tone images for the pilot image selection experiment. These images can be stored in a document oriented database (e.g. MongoDB). A database has the advantage that information such as what preprocessing steps have been applied, what license information an images has, what is the average reaction time of the images in specific experiments etc. can be stored among the images. In addition images can be searched and selected according to these information. In this pilot experiment human subjects were presented with the two-tone, Mooney image and were asked to indicate the time when they recognized the hidden object in the image with a key press. They were further asked to label the name of the object that they think they recognized. 

In our functional magnetic resonance imaging (fMRI) experiment we were interested in the question how brain activity changes when subject's recognize the hidden object versus when they not. The two-tone images do not change over the course of the presentation but subject's perception change over time and this moment in recognition is associated with a change in brain activity, which we wanted to capture. FMRI image acquisition is relatively slow (every 2 seconds). In addition, as fMRI scans are costly, we are limited by time. Hence, for this fMRI experiment I selected 120 Mooney images (resized to have a 400×400 pixel size) that were recognized within 4-10 seconds in the pilot experiment.

The code (written in python) to create new two-tone, Mooney images are available on github.

##### Pain points

When images are downloaded from an online resource copyright issues can emerge. This can be avoided by downloading images that are licenced as Creative Common. This change is reflected on the latest version controlled pymooney code and new images can be created with such criteria.

##### Key benefits

The main benefit of this part of a larger experiment is that these images are now available for further research. The images are currently used in 30 different experiments ranging from clinical set-ups, human memory experiments, vision research, and latest internet security applications.

##### Key tools

Image processing libraries are important building blocks of this particular case study. In this case the open source python library scikit-image was used. In addition online image database APIs such as FlickrAPI are essential.

##### What does "reproducibility" mean to you in general and/or in the particular context of your case study?

In the context of this study reproducibility means that given the code and a database of images, a new researcher can have access to the images and use the code that was used to create the same images or new images with the same parameters. These images can then be used to (i) replicate the current findings, (ii) create new questions potentially based on the current findings.

##### General questions about reproducibility [Optional]

1) Why do you think that reproducibility in your domain is important?

Not only in my domain but in general I think without reproducible research we waste a lot of professinal time and research money. In my own domain, and in direct connection to this case study I can outline an example. When I came upon the two-tone images in the literature, I contacted several groups with a request to use their images (Of course I mentioned that I will properly cite their work), who had used similar images for other behavioral or neuroscience experiments. Unfortunately, the images that these groups used were very limited in number but nevertheless, I never got a response from these groups. Hence, in order to start with my experiment I had to spend almost a year to create the new stimuli.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

This was a self thaught practice. Hence, the stage it is described here still has some space for improvement, which I will elaborate further below.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

In general, in neuroscience the main pitfalls are sharing of human subject data and the resistance in the field to share code (or images in this case). The majority of the community does not have the mind set to that is similar to open source. Researchers are afraid that someone else can conduct an experiment before they publish their results. Even if they published some results they are sometimes not willing to share the data as they think they can continue to ask new questions.

4) What do you view as the major incentives for doing reproducible research?

I think reproducible research allows progress not only in the own domain but also makes interdisciplinary projects possible. To see that your own research is further used not only in your own domain but also across domains is very rewarding.

