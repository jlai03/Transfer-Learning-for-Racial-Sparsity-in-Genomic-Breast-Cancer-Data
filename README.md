# Transfer Learning for Racial Sparsity in Genomic Breast Cancer Data

### STEP 1: Sort Data Script (under data_preparation)

    FILE NAME: sort_data.ipynb

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
                      

### STEP 2: Sort Labels Script (under data_preparation)

    FILE NAME: sort_labels.ipynb

    TSV Data under data/raw_labels contains every single column in clinical data. 
    This script filters for the following columns: 
    - 'case_id'
    - 'age_at_index'
    - 'gender'
    - 'race'
    - 'ajcc_pathologic_stage'
    - 'primary_diagnosis'
    - 'prior_malignancy'

    Filtered tsv file is written out to data/processed_labels

### STEP 3: Prepare Model Data Script (under data_preparation)

    FILE NAME: prepare_model_data.ipynb

    - Each sample is filtered for only [chromosome number, CNV number, and gene length]
    - Then each sample's chromosome numbers is one hot encoded
    - All the samples are saved into a dataframe. Each row contains the [race, sample data, diagnosis] of a given sample
    - dataframe saved to data/model_data.pkl

### STEP 4: Baseline models (under baseline_models)

    Here, the model data dataframe is loaded from data/model_data.pkl and processed for training / testing for each script. 

    Under baseline_models, we train the following models on data from white patients and 
    test it on black + african american patients, and asian patients spearately. 
    These are the trials for collecting baseline metrics (per recommendation of TA). 

        - DNN 
        - LSTM 
        - Transformer 
        - SVM 
        - XG Boost

    Each script contains code to run a single trial of each model. Reported results aggregates 
    avg. across 50 trial runs. 

### STEP 5: Transfer Learning models (under transfer_learning_models)

    Here, the model data dataframe is loaded from data/model_data.pkl and processed for training / testing for each script. 

    Under transfer_learning_models, we train the following models on data from white
    patients and leverage transfer learning accordingly to test on data from black + 
    african american patients, and asian patients separately. 

        - DNN 
        - LSTM 
        - Transformer 

    These scripts test model behavior for two transfer learning techniques: (1) fine tuning alone, 
    as well as (2) freezing layers + fine tuning. Each script contains code to run a single trial 
    of each model. Reported results aggregates avg. across 50 trial runs. 

# DATA ANALYSIS 

### clinical_data_analysis (under analysis)

    This script currently looks at the distribution of the primary diagnosis. It also demonstrates a notable difference
    between infiltrating ductal carcinoma, lobular carcinoma, infiltrating ductal & lobular carcinoma, and other rarer types

    End of script displays the distribution of race amongst the sample data. 
