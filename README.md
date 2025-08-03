# TFTG
Identification of indication specific transcription factors

AIM: To understand how a given transcription factor performs across multiple indications


STEPS:




**1) Find a reliable database that has data on Transcription factor and its respective targets with proper experimental backup**


Database chosen for this study: TRRUST


-> Experimentally validated


-> small dataset


-> Contains data on actual regulation and not predictions


-> PMID supported





**2) Download the mRNA expression dataset for indication of choice from Cbioportal**


Indications tested in this case scenario: 

--> Invasive breast cancer

--> Adenocortical carcinoma

--> Cholangiocarcinoma (PancancerAtlas)




**3) Filter the TF-TG from the dataset:**


Detailed step by step explanation with the code


Platform used for analysis: Google collab


Download the mRNA dataset for the indication of interest: Go to cbioportal and download the tar.gz file for the indications of interest

-----------

*1) Download the dataset from cbioportal :* 

!wget https://cbioportal-datahub.s3.amazonaws.com/acc_tcga_pan_can_atlas_2018.tar.gz


=> wget is a command-line utility for retrieving content from web servers.


https://cbioportal-datahub.s3.amazonaws.com/acc_tcga_pan_can_atlas_2018.tar.gz is the URL of the file to be downloaded.


This command downloads the gzipped tar archive named acc_tcga_pan_can_atlas_2018.tar.gz from the specified URL.

----------------------------------------

*2) Unzip the tar file:* 

!tar -xvzf acc_tcga_pan_can_atlas_2018.tar.gz

=> tar is a command-line utility for working with tar archives.


-x is an option to extract files from an archive.


-v is an option for verbose output, which means it will list the files as they are extracted.


-z is an option to decompress the archive using gzip.


-f is an option to specify the input archive file, which in this case is acc_tcga_pan_can_atlas_2018.tar.gz.


So, this command extracts the contents of the gzipped tar archive named acc_tcga_pan_can_atlas_2018.tar.gz and lists the files as they are extracted.

-----------------------------------------------------------

*3) Load the mRNA data of the genes and samples in pandas dataframe:*

import pandas as pd


import numpy as np


from scipy.stats import pearsonr


import scipy.stats as stats


file_path = 'acc_tcga_pan_can_atlas_2018/data_mrna_seq_v2_rsem.txt'


df = pd.read_csv(file_path, sep="\t", comment='#')


=> Import Libraries: Imports pandas, numpy, and statistical tools from scipy.stats for data handling and analysis.


Set File Path: Defines file_path pointing to the data file.


Load Data: Uses pd.read_csv() to load a tab-separated file into a DataFrame (df), skipping comment lines (starting with #).

----------------------------------------------------------------------

*4) Load the data from the transcription factor target database and load it into pandas dataframe:*


!wget https://www.grnpedia.org/trrust/data/trrust_rawdata.human.tsv


import pandas as pd


import numpy as np


from scipy.stats import pearsonr


import scipy.stats as stats

 
file_path = 'trrust_rawdata.human.tsv.1'


df = pd.read_csv(file_path, sep="\t", comment='#')

-------------------------------------------------------------------------------------------

*5) Assign headers to the dataframe*


df_trrust.columns = ['TF', 'TG', 'impact', 'PMID']


display(df_trrust.head())

-------------------------------------------------------------------------------------------

*6) Export the datafile as an excel file to analyse*


df_trrust.to_excel('trrust_data.xlsx', index=False)

from google.colab import files


files.download('trrust_data.xlsx')


-------------------------------------------------------------------------------------------


