---
published: true
layout: post
tags:
  - databases
  - postgreSQL
  - windows
excerpt: >-
  The MIMIC II database is an excellent resource with thousands of de-identified
  ICU patients and their EMR data. Installation of the database for Windows is a
  bit sparse so here is some more information on how to get it working. 
comments: true
---
## Installing MIMIC II Database on Windows

[MIMIC II](https://physionet.org/mimic2/), Multiparameter Intelligent Monitoring in Intensive Care, is a database with approxmiately 33,000 de-identified patients. It is available for public use (after submitting an application) and is free to use. This makes the MIMIC database an excellent resource for researchers and data analysts alike to use and build machine learning models or run statistical analyses for specific medical conditions that would otherwise be unaccessible. 

A new version of the MIMIC database, MIMIC III, is [available online](https://mimic.physionet.org/tutorials/install-mimic-locally-windows/) and has thorough documentation on how to install the database for different systems. 

Documentation for MIMIC II is also available, but it's not as thorough as it could be for Windows users. When you download MIMIC II, it comes with shell scripts to use on unix/linux/OS X machines, but fortunately there is a [python script to run in Windows](https://github.com/AndreaBravi/MIMIC2) available. A few extra steps are needed to clarify how to use this python script. 

* Be sure you have already installed PostrgreSQL. I used version 9.6.1 without issue. 
* Have python installed on your workstation. My machine already has Anaconda which installed Python. 
* If you're planning on installing the entire database, you're supposed to have at least 75GB. 
* **Most importantly, you must place the files files (the tar.gz files) into the MIMIC-Importer-2.6/tarballs directory. Include in this directory the mimic2cdb-2.6-Definitions.tar.gz file as well! **

1. Download the [python script](https://github.com/AndreaBravi/MIMIC2). 
2. If you downloaded the script in your Downloads folder, then you will need to launch the Command Prompt window and type the following: 
</pre>python.exe C:\Users\YOURUSERNAME\Downloads\MIMIC2-master\MIMIC2-master\mimic2_setup.py</pre>
3. If python.exe does not work, then you will need to set up your PATH variable to load Python, or point directly to the python executable. 
4. The script will ask for **script to pg_env.bat:**. This is referring to the Postgres installation directory. For me I typed: 
<pre>C\Program Files\PostgreSQL\9.6</pre>
5. Now you will be asked for **Provide Path to MIMIC Importer:**, which is the script that comes from MIMIC's website where you download the flat files (it is not included with the flat files). For me I saved it to my desktop: 
<pre> C:\Users\darene\Desktop\MIMIC\MIMIC-Importer-2.6</pre>
6. The script will ask for the database credentials you'd like to use. 
7. Finally, it will untar the tarballed flat files which will take a few minutes, and then proceed with adding each subject to the database. 

If you have any trouble, the included README.txt that's included with the flat file download is very thorough.
