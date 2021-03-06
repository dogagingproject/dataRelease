### Dog Aging Project | Tips for working with survey data files

##### CSV files:
* This data format gives users access to the raw data field names and values.  
* The original survey question text and value labels for each variable can be found in the accompanying CODEBOOK file. 
  * For example, for the field "dd_breed_pure_or_mixed" contained in `DAP_[year]_HLES_dog_owner_[datasetVersion].csv`, one can see raw data values of 1 or 2.  Referring to `DAP_[year]_CODEBOOK_[datasetVersion].csv`, one can see that the corresponding survey  question text is “Is your dog a purebred or mixed breed”, and that the raw data values of 1 or 2 correspond to value labels of “Purebred” or “Mixed breed”, respectively.  

*** 

##### R files:
* The .RData uses labelled variables from the haven package, which you will need to install in order to use the data in R. 
* This data format gives users access to the original survey question text, the raw data values, and value labels for each variable in the data sets. 
  * For example, for the question “Is your dog a purebred or mixed breed”, the values are 1 or 2, and the labels are “Purebred” or “Mixed breed”.  
* [DAP .RData USER GUIDE](https://github.com/dogagingproject/survey_instruments/blob/main/TERRA_support_docs/DAP_RData_Readme.pdf) : walks through how to use labeled variables and transform them into integer or factor variables.
* String variables are limited to 2,040 characters. Full string variable text is available in the CSV format. 

***

##### STATA files:
* The .dta includes raw data values and values labels (1 or 2 and “Purebred” or “Mixed breed”), as well as the original survey question text (“Is your dog a purebred or mixed breed”). The variable label contains as many characters from the question as would fit. See each variable's “Notes” for complete question text.
* String variables are limited to 2,040 characters. Full string variable text is available in the CSV format.
* Due to STATA limitations, variable names are truncated to 31 characters.  Shortened names that are duplicated have “_01, 02, etc.” appended at the end of the variable name.

***

##### SPSS files: 
* The .sav includes raw data values and values labels (1 or 2 and “Purebred” or “Mixed breed”), as well as the original survey question text (“Is your dog a purebred or mixed breed”) in the variable label.
* In SPSS only, string variables are limited to 255 characters. String variables for longer open-ended text questions will run over into extra variables, each 255 characters in length. 

*** 

###### *last updated 2022-06-10*