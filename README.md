# MIMIC IV to OMOP CDM Conversion #

### What is this repository for? ###

* Quick summary
* Version
* [Learn Markdown](https://bitbucket.org/tutorials/markdowndemo)

### How do I get set up? ###

* Summary of set up
* Configuration
* Dependencies
* Database configuration
* How to run tests
* Deployment instructions

### Contribution guidelines ###

* Writing tests
* Code review
* Other guidelines

### Who do I talk to? ###

* Repo owner or admin
* Other community or team contact

### Change Log (latest first) ###


**2020-11-16**

* TUF-10 Basic logic for CDM tables based on MIMIC-III logic
    * TUF-19 Measurement - Rule 3 (microbiology) - done (without tests)
        * Mapping for antibiotic susceptibility is done
    * TUF-19 Measurement - Rule 2 (chartevent) is started
    * TUF-20 Death table - done
    * TUF-51 Device_exposure - done with Rule 1 lk_drug_mapped
    * TUF-58 Specimen - done (without tests)
* TUF-76 Bugfix according to Achilles Heel Report
    * Person count - done
    * Condition mapping rate - done
    * Observation periods - done
    * Open points:
        * Observation value_as fields all null
        * Event dates before year of birth
* TUF-75 Basic Orchestration
    * run_workflow.py is added
    * Variables section is added to configs for bq_run_script.py and run_workflow.py
    * Dataset names are replaced in ut/\*.sql and qa/\*.sql
    * Nice output is added to bq_run_script
    * Fixed: dealing with quotes (") inside a query
    * Known issue: do not use semicolon (;) inside comments


**2020-10-26**

* TUF-10 Implement basic logic based on MIMIC III conversion
    * Tables implemented: 
        cdm_location, care_site, cdm_person, 
        cdm_visit_occurrence, cdm_visit_detail, 
        cdm_condition_occurrence, cdm_procedure_occurrence, cdm_measurement, cdm_drug_exposure, cdm_observation, cdm_device_exposure
        cdm_observation_period, cdm_cdm_source
* TUF-75 Implement basic orchestration
    * configuration design - in progress
    * Real dataset names are replaced with variables
    * folders structure is changed


**2020-09-21**

* TUF-10 Implement basic logic based on MIMIC III conversion
    * Tables implemented: cdm_person, cdm_care_site, cdm_location, cdm_visit_occurrence
    * Tables in progress: cdm_visit_detail, cdm_death
* TUF-11 Load Vocabularies
    * Athena vocabularies are loaded to `vocabulary_2020_09_11`

Start development
* The project includes:
    * folders
    * DDL script
    * vocabulary_refresh scripts set

### The End ###


### Concepts / best practice / lessons learned ###

* keep vocabularies in a separate dataset standard, and add custom mapping each time vocabs are copied to the cdm dataset? 
    * usual practice: apply custom mapping to vocabs in the vocab dataset
    * plus of this alternative: no clean-up is neede, we just add the custom concepts
* working on a task, 
    * create a branch / complete prev PR
    * declare a comparison dataset, i.e. the result of previously completed task
    * create a new working dataset named mimiciv_cdm_task_id_developer_yyyy_mm_dd
    * create a UAT dataset when a significant piece of work is completed and tested
        * the name is mimiciv_uat_yyyy_mm_dd
        * uat = copy of the best and lates cdm
    * cleanup cdm datasets when uat is created or earlier if they are not needed anymore

