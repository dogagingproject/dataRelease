### Dog Aging Project | Samples Results Metadata User Guide

The Clinical Lab Data Metadata contains information surrounding the circumstances of clinical lab sample collection and the condition of the relevant samples upon receipt by the responsible labs. These data have been curated to provide the best available information given the potential for sample collection across multiple clinic visits and missing data.

These columns are constructed in the following manner:

| Variable      | Description | Possible Values | 
| :--- | :----- | :------------- | 
| `dog_id`      | Unique identifier for given dog. | Integer | 
| `Sample_DogSize`      | Dog size for sampling. <br><br>For small dogs (generally <15lb): <br> - Chemistry panel, urine, metabolome and micriobiome samples are collected at clinic visit 1. <br>  - CBC, flow cytometry, and RRBS samples are collected at clinic visit 2 (approximately 6 weeks after clinic visit 1).<br><br>For large dogs, all samples are collected in single clinic visit. | Large <br> Small | 
| `Sample_Year`      | Sampling year derived from REDCap event.       | precision_1<br>precision_2<br>precision_... | 
| `Sample_Type`      | Sample type.  | CBC<br>Chemistry Panel<br>Flow Cytometry<br>Metabolome<br>Microbiome<br>RRBS<br>Urine |  
| `DAP_Sample_ID` | Unique identifier for given sample. This variable should be used to match to sample results files. | Various numeric or string formats depending on `Sample_Type` |
| `Sample_Collection_DateTime`  | Date/time of sample collection as recorded at relevant clinic visit.<br><br>(1) As recorded by clinic.<br><br>(2) If (1) is not available, 12pm on the owner provided clinic visit date.  | YYYY-MM-DD HH:MM:SS |  
| `Sample_Dog_Hours_Fasted`<sup>1</sup> | Number of hours dog was fasted prior to sample collection. | Integer | 
| `Sample_Dog_Weight`<sup>1,2</sup>   | Dog's weight. | Numeric | 
| `Sample_Dog_Weight_Units`<sup>1,2</sup>   | Units for dog's weight. | kg <br> lb | 
| `Sample_Dog_Body_Condition_Score`<sup>1,2</sup>   | Body condition score recorded. | Integer | 
| `Sample_Dog_Body_Condition_Score_Scale`<sup>1,2</sup>   | Scale used for body condition score. | Out of 5 <br> Out of 9 | 
| `Sample_Dog_Blood_Transfusion_Ever`<sup>1</sup>   | Was a blood transfusion in dog's history reported at the clinic visit? | Yes<br>No<br>Unknown |  
| `Sample_Dog_Blood_Transfusion_Past3Mo`<sup>1</sup>   | Was a blood transfusion within the past 3 months reported at the clinic visit? | Yes<br>No<br>Unknown | 
| `Sample_Dog_Medications_Past_Week`<sup>1</sup>   | Medications reported to have been administered to the dog within the week preceding the clinic visit. | Text | 
| `Sample_Fecal_Collection_Method`<sup>1</sup>   | If relevant, method of fecal sample collection recorded at relevant clinic visit. | Voided<br>Collected during rectal exam<br>Unable to collect fecal sample |  
| `Sample_Urine_Collection_Method`<sup>1</sup>   | If relevant, method of urine sample collection. | Free catch (preferred)<br>Cystocentesis<br>Catherization<br>Unable to collect urine sample |     
| `Sample_Ease_Blood_Draw`<sup>1</sup>   | Ease of blood draw. | Unable to draw blood<br>1 - nearly impossible to find vein; multiple attempts needed<br>2 - very difficult to find vein; 3-4 attempts needed<br>3 - moderately difficult to find vein; 2-3 attempts needed<br>4 - mildly difficult to find vein; 1-2 attempts needed<br>5 - blood drawn on first attempt; no issues  
| `Sample_Dog_Attitude`<sup>1</sup>   | Overall attitude of dog at time of sample collection. | 1 - extremely uncooperative or agitated <br> 2 - very difficult to keep patient still <br> 3 - moderately difficult to keep patient still <br> 4 - mildly difficult to keep patient still <br> 5 - cooperative and calm  | 
| `Sample_Processing_DateTime`  | Relevant DAP processing date/time.<br><br>(1) If available, this is the arrival (CBC, Chemistry Panel, Microbiome) or location/final (Urine, Flow Cytometry, Metabolome, RRBS) date/time.<br><br>(2) For sample types other than CBC and Flow Cytometry, if (1) is not available, arrival/location/final scans of other sample types arriving with the sample of interest are used.<br><br>(3) For CBC, or for other sample types if (2) is not available, the relevant kit's arrival scan is used.  | YYYY-MM-DD HH:MM:SS | 
| `Sample_Processing_DateTime_Source_Type`  | Source used for `Sample_Processing_DateTime`. | Processing date/time of specified sample<br>Processing date/time of proximate sample<br>Processing date/time of kit containing sample |  
| `Sample_Processing_DateTime_Source_Details`  | Describes REDCap source variables for `Sample_Processing_DateTime`. | Text |  
| `Sample_Arrival_Temperature`  | Temperature of sample upon arrival to DAP.<br><br>(1) Arrival temperature of relevant sample.<br><br>(2) If (1) is not available, average arrival temperature of samples arriving in same kit. | Numeric | 
| `Sample_Arrival_Temperature_Source_Type`  | Source used for `Sample_Arrival_Temperature`. | Arrival temperature of specified sample<br>Arrival temperature of proximate sample<br>Average arrival temperature of proximate samples | 
| `Sample_Arrival_Temperature_Source_Details`  | Describes REDCap source variables for `Sample_Arrival_Temperature`. | Text | 
| `Sample_Arrival_Condition`  | Condition of sample upon arrival. | Clotted<br>Leaking<br>Normal<br>NA | 
| `Sample_Hemolysis`<sup>3</sup>  | Hemolysis reported for relevant sample (Chemistry Panel and Metabolome only). | None<br>+1<br>+2<br>+3<br>+4 | 
| `Sample_Lipemia`<sup>3</sup>  | Lipemia reported for relevant sample (Chemistry Panel and Metabolome only). | None<br>+1<br>+2<br>+3<br>+4 | 
| `Sample_Icterus`<sup>3</sup>  | Icterus reported for relevant sample (Chemistry Panel and Metabolome only). |  None<br>+1<br>+2<br>+3<br>+4 |
<br>

<sup>1</sup> Data for this field is included if recorded by the veterinary clinic at time of sample collection.  
<sup>2</sup> These fields were not formally part of the data collection sheet used by the veterinary clinic at time of sample collection until August 2022. For samples collected before that time, nearly all will have NA for these fields.  
<sup>3</sup> Symbols may not display when viewed in Excel.

### Additional resources 
Reference ranges for CBC and chemistry panel can be found in the [Clinical Lab Data Reference Intervals](https://github.com/dogagingproject/dataRelease/blob/master/Supporting_Documents/DAP_Clinical_Lab_Reference_Intervals.md)  

For detailed sample collection methodology refer to: <b>Prescott, J., Keyser, A.J., Litwin, P. et al. Rationale and design of the Dog Aging Project precision cohort: a multi-omic resource for longitudinal research in geroscience.GeroScience (2025). https://doi.org/10.1007/s11357-025-01571-3</b> 

*** 

###### *last updated 2025-03-13*