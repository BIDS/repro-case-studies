##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Anthony Arendt and I hold a joint appointment as a Senior Research Scientist at the Applied Physics Laboratory, and a Research Fellow at the eScience Institute, University of Washington. I am part of a research team that studies the impact of glaciers on rising global sea levels, with a focus on the glaciers of Alaska and northwestern Canada. During the past 20 years my colleagues at the University of Alaska Fairbanks have been measuring the elevation changes of Alaska's glaciers using LiDAR data collected from a small aircraft. We use these data to estimate total changes in mass of each observed glacier, and then extrapolate these data to unmeasured glaciers based on information acquired from satellite imagery. From this we produce detailed maps of the spatial distribution of glacier mass change and the total contribution of these ice masses to global ocean change.

During the 20 year duration of the project the data analysis has evolved from manual manipulation of text files, to a semi-automated workflow that integrates GIS, relational database and Python tools within a cloud computing framework. Here we describe the workflow which culminated in a recent publication (Larsen et al., 2015). Core developers of the software include Evan Burgess, Christian Kienholz, Justin Rich, Anthony Arendt and Christopher Larsen. 

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

Reproducability is a crucial component of our workflow due to the dynamic nature of our monitoring campaign, and the need to constantly update the position and elevation of glaciers as they change in response to climate. We achieve reproducability through: 

+ maintaining consistency in the input datasets
+ utilizing a series of scripts to automate data ingest and filtering
+ storing raw and filtered/processed data in a relational database
+ generating data objects that handle typical data analysis functions
+ scripting all manuscript figures in Jupyter notebooks.  

##### Workflow diagram
 
See attached workflow diagram: altimetryReproducability.html

##### Workflow narrative

The workflow begins with annual field data collection that produces both GPS positional and LiDAR point cloud data, both in  industry standard binary formats. Commercial proprietary software is used to process the data into four dimensional point observations (x, y, z and time), which are then further processed and filtered using Matlab scripts into gridded 10 m digital elevation models. These elevation maps are then differenced with maps from an earlier flight to obtain a change in elevation along the flight line. These results are stored in text files, with the filename describing the glacier name and start and end dates, and are located on a local server at the University of Alaska Fairbanks. In a separate step, we assemble satellite imagery and regional digital elevation models for the Alaska region. We use ArcGIS to manually digitize glacier extent, and Python scripts (using the arcpy library) to calculate the distribution of glacier surface area with elevation for each of approximately 27,000 glaciers in Alaska. 

The majority of our data processing and analysis occurs on a single Microsoft Azure Linux Virtual Machine that hosts a spatially enabled relational database and a series of Python scripts used to process and manipulate the data. The VM hosts a PostgreSQL database with the PostGIS extension, to which we ingest point, line and polygon geospatial datasets. Relevant tables include: 

+ _inventory_: polygons of each glacier in Alaska with attributes of surface area, glacier type (whether terminating on land or ocean), name 
+ _regions_: polygons of outlines of mountain ranges or climatic zones over which we perform regional extrapolations
+ _LiDAR_: stores the altimetry elevation and volume changes on surveyed glaciers
+ _extrapolatedResults_: final estimates of the volume change of every glacier in Alaska

Each time we have new altimetry observations we run a Python script to:

+ connect via secure FTP to the server in Fairbanks and search for new text files across the directory structure ingest each text file into a Pandas dataframe
+ insert the new data into rows of the _LiDAR_ table via database connections through SQLAlechmey
+ generate simple plots from Pandas to visualize and quality check the ingested datasets. 

Similar Python tools are used to create and update the _inventory_ and _regions_ tables, for example to accommodate changes in surface area as glaciers retreat.

The _LiDAR Data Object_ is the foundation of all subsequent processing and analysis. The data object is created via a function call with parameters describing a single or a regional grouping of glaciers. Each instance of the data object has predefined attributes enabling users to rapidly acquire elements of the raw data in the _LiDAR_ table. For example, a user can issue a request to the _LiDAR_ table for a specific glacier, returning a data object whose attributes contain that glacier's elevation change, area, and other statistical information, and use this to make plots or perform analysis. The data object also has several methods that handle the majority of the standard data processing and filtering workflow. These methods include:

+ _normalizeElevation_: converts from actual to normalized elevation ranges to facilitate comparison between glaciers
+ _calcStats_: generates statistics on the distribution of elevation change observations
+ _fixTerminus_: accounts for the adjustment of elevation change data in the case of a rapidly retreating glacier
+ _calcMassBalance_: generates the glacier-wide change in mass of each glacier. 

In a final processing step, we utilize the grouping functionality of the LiDAR object methods to generate average elevation change profiles across glaciers grouped by type or by spatial location. For example, we found similar elevation change distributions across glaciers with similar terminus types (i.e. whether terminating in land or in water). Therefore we generated LiDAR objects averaged over _type_ groupings, as queried from our _inventory_ table, thereby returning a single estimate of elevation change versus elevation. In a final step, we invoked a function that regionally extrapolated these profiles to the unmeasured ice masses stored in the _inventory_ table, based on their distribution of area with elevation. This returns a dictionary of ice mass changes by group, as well as an optional new database table containing mass change estimates for each of the 27,000 ice polygons in the region (table _extrapolatedResults_). All functions and methods run quickly, with the exception of steps involved in building _extrapolatedResults_, which takes about 15 minutes to run. 
 
To analyze results and distribute our findings we hosted a permanent instance of a Jupyter notebook on our Linux VM and provided access to project team members. The notebooks, as well as the core Python scripts used to generate results, are also located in a github repository. The notebook also contained markdown to provide metadata at each step in the analysis. 

E. Burgess generated the majority of the Python code to build plots and perform analysis for the manuscript. J. Rich and C. Kienholz were involved in the integration of the _inventory_ tables with the LiDAR workflow. During manuscript creation E. Burgess integrated adjustments to the code at the request of other team members, in response to plots and tables shared via e-mail. A. Arendt has subsequently worked to streamline the usability and automation of the workflow to help non-experts gain access to the most important tools. Since the manuscript was published, we have shared access to our database with other researchers. For example, collaborators with experience in SQL have direct access to the PostgreSQL database to perform their own queries, while other collaborators more familiar with GIS tools are connecting directly to the geospatially encoded tables to generate maps.   

As required by our NASA funding agency, our raw data are also provided online, but none of the higher level (e.g. extrapolated) products are online, and our github pages are still incomplete with respect to distributing all of our processing tools and methods. Only a small handful of close collaborators are aware of these tools. However, all of our functions are well documented, and the overall framework was designed with reproducability in mind. Efforts are ongoing to finalize a distribution library that will include example datasets and full documentation.  


##### Pain points

Our team brought together researchers with different backgrounds and approaches to data handling and processing. The processing of raw LiDAR and GPS data is performed by a different group than the one handling the GIS and extrapolation portion of the project, and each uses different software tools. We dealt with this problem by creating standardized files at different stages of the processing chain. For example, the LiDAR/GPS team produced a stack of files processed to the point where they could be used for extrapolation, which were then ingested to the geospatial database. A challenge here is the data are replicated in multiple locations, requiring careful version control. 

Another challenge is that Alaska is a difficult place to set up a cloud computational framework. Connection speeds to Microsoft Azure resources are slow from Alaska due to bandwidth limitations. We therefore performed our initial database design on local Alaska servers, but this created complications when collaborators from federal agencies tried to share our resources, due to firewall limitations. At present we still maintain a local server in Alaska that is a duplicate of the Azure resources being maintained by A. Arendt in Washington. This creates headaches with respect to database management. 

##### Key benefits

+ our workflow provides a mechanism to continually update our analysis as new data arrive. Our project is funded for several more years, and we are now in a position to regenerate key figures and update sea level estimates every time we acquire new datasets. This will greatly diminish the time it takes for us to provide stakeholders with updated information on the status of Alaska glaciers and their contribution to sea level. Also, our data are uniquely dynamic, and must accommodate not only new data but changes to the base inventory as glacier geometries (area and elevation) change over time. By having all our inventory data in relational tables we can update individual polygons and account for the feedback effects of glacier area on mass balance. 

+ our workflow provides a stable foundation that can accommodate changes in team composition over time. E. Burgess was a postdoctoral researcher who has now left the project, but thanks to his scripting and documentation we are able to build on his efforts, rather than having to reinvent things from scratch. 

+ we are well positioned to explore our data in ways not previously possible. New collaborators are joining our team and making direct connections to our database, generating complex queries that are exploring what climatic and geometric factors may be driving the glacier mass changes we are observing in the field. Other similar LiDAR observation programs do not provide access to relational databases, limiting researchers' ability to perform spatial and temproal queries. 

+ our approach is helping to minimize blunders in processing and enables all team members to check on each other's work.

##### Key tools

Hosting our resources in a cloud environment played a vital role in making our workflow reproducable. We strongly recommend investigating in one of the many cloud hosting environments currently available to researchers. 

##### General questions about reproducibility

1) Why do you think that reproducibility in your domain is important?

Glaciology has become highly interdisciplinary in the past decade: oceanographers, climatologists, geodesists and glaciologists must integrate knowledge to solve the sea level problem. Also, data from remote glacier regions is sparse, so any data we collect needs to be made available. By generating reproducible workflows we have a greater capacity to share information and to better understand exactly how each research team is processing their datasets.

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

I learned these techniques through on-the-job training and classes.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

The inability of non-specialists to make full use of our tools requires us to revert back to non-reproducible methods in order to get things done in a timely fashion. For example, many researchers in our domain use Matlab, and cannot take the time to learn Python, which is the core of most of our scripts. We are working to solve this problem by building lightweight Application Programming Interfaces enabling collaborators to access some of the core elements of our workflow through simple web protocols.

4) What do you view as the major incentives for doing reproducible research?

Within a research team, major incentives include: increased transparency in methods, increased accountability and ability to check for errors in processing, a reduction in spin-up time as new members join the team, and an ability to minimize duplication of effort. Between the team and other collaborators/stakeholders, we see major benefits in the ability to share and visualize results, and in our capactiy to perform cross-disciplinary research. 

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

We recommend development and adherence to standards in geospatial data formats and distribution protocols. 

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?
