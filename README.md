# MAIN PIPELINE

### STEP 1: Sort Data Script (under sorting_scripts)

    Data under data/raw_data looks like: 
        
        raw_data ----- sample_id1 --- .tsv file 
                |___ sample_id2 --- .tsv file 
                |____ ....
                .
                .___ sample_idn --- .tsv file 

    This script sorts the tsv files by storing each tsv file under their respective case ID's (i.e. patient ID). 
    So the processed data files will be stored under data/processed_data like this: 

        processed_data ------ case_id1 ----- .tsv file 1 
                        |           |_____ ..... 
                        |           . 
                        |           ._____ .tsv file n 
                        |
                        |
                        |
                        |__ case_id2 ----- .tsv file 1 
                        |           |_____ ..... 
                        |           . 
                        |           ._____ .tsv file n 
                        |
                        . 
                        .
                        .___ case_idx ----- .tsv file 1 
                                    |_____ ..... 
                                    . 
                                    ._____ .tsv file n 



    NOTE: This script queries GDC Endpoint for Case ID
                      

### STEP 2: Sort Labels Script (under sorting_scripts)

    TSV Data under data/raw_labels contains every single column in clinical data. 
    This script filters for the following columns: 
    - 'case_id'
    - 'age_at_index'
    - 'gender'
    - 'ajcc_pathologic_stage'
    - 'primary_diagnosis'
    - 'prior_malignancy'

    Filtered tsv file is written out to data/processed_labels

### STEP 3: Main.ipynb 

    At this step, we've processed the input CNV data as well as the clinical data with each patient's primary diagnosis. 
    Hopefully we can train the models here. 


# DATA ANALYSIS 

### clinical_data_analysis (under analysis)

    This script currently looks at the distribution of the primary diagnosis. It also demonstrates a notable difference
    between infiltrating ductal carcinoma, lobular carcinoma, infiltrating ductal & lobular carcinoma, and other rarer types