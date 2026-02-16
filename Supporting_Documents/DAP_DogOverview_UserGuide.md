## Dog Aging Project | Dog Overview User Guide

This document provides an introduction to the Dog Overview dataset using an example dog from the 2025 Curated Data release.

### Dog status

This section provides basic information about the dog, including its unique identifier, when the dog became a member of the DAP Pack, and details about the dog's enrollment in a cohort (if relevant).

| Variable      | Description | Possible Values |
| :--- | :---------------------------- | :------------------------------- |
| `dog_id`      | Unique dog identifier       | Integer | 
| `DAP_Pack_Date` | Date of HLES completion | YYYY-MM-DD |
| `Cohort` | Dog's enrolled cohort, if any | DAP Pack <br> Foundation <br>  Precision <br> Precision - Brain Health Study|
| `Cohort_Enroll_Date` | Date enrolled in Foundation or Precision Cohort (if applicable) | YYYY-MM-DD |

Using `dog_id` 33975 as an example, we can see that the dog became a member of the DAP pack on 2020-10-13, and was enrolled in the Precision cohort on 2021-06-21.

| dog_id | DAP_Pack_Date | Cohort | Cohort_Enroll_Date |
| :--- | :------------------ | :-------------------- |  :------------------- |
| 33975 | 2020-10-13 | Precision | 2021-06-01 |


### Dog demographics

This section provides details regarding  basic characteristics of a given dog, such as date of birth, sex, breed, and date of death (if relevant), as well as dog demographic reporting classifications (see relevant section for details).

#### Estimated age and DOB

In HLES, owners are asked to provide their dog's birth year (and month, if known), or, at the very least, their dog's age. Using that information along with the date of HLES completion, a dog's DOB and age at HLES can be estimated by the following methods.

| Owner provided      | DOB estimation method | Age estimation method |
| :--- | :---------------------------- | :------------------------------- |
| Birth year and month | Use birth year and month; assume 15 for day unless birth year and month are same as year and month of `DAP_Pack_Date`, in which case assume 1 for day | Difference between estimated DOB and HLES completion date |
| Birth year only | Use birth year; if birth year != HLES completion year, assume 6 for month and 15 for day; otherwise assume midpoint between January 1st and HLES completion date | Difference between estimated DOB and HLES completion date |
| Age | Subtract age from HLES completion date | Use owner-reported age | 

These estimation methods are used to define the following variables.

| Variable      | Description | Possible Values |
| :--- | :---------------------------- | :------------------------------- |
| `Estimated_DOB`      | Best available estimate of DOB at HLES       | YYYY-MM-DD |
| `Estimated_Age_Years_at_HLES` | Best available estimate of age at HLES | Numeric |
| `AgeDOB_Estimation_Method` | Method used to estimate DOB and age |  Estimated using owner-reported age <br> Estimated using owner-reported birth year <br> Estimated using owner-reported birth year and month |

Going back to our example dog, we see that age and DOB were estimated using owner-provided birth year only. The owner indicated that the dog was born in 2010. The birth year and year of HLES completion are different, so we assume the birth month to be June and the birth day to be the 15th, resulting in an estimated DOB of 2010-06-15. If we subtract the estimated DOB from the date of HLES completion (which is the same as the DAP Pack date), we estimate the dog's age at HLES to be 10.3 years. 

| dog_id      | DAP_Pack_Date | Estimated_DOB | Estimated_Age_Years_at_HLES | AgeDOB_Estimation_Method | 
| :--- | :------------------ | :-------------------- |  :------------------- | :------------ |
| 33975 | 2020-10-13 | 2010-06-15 | 10.3 | Estimated using owner-reported birth year | 

#### Dog breed(s)

This section provides information regarding owner-reported purebred or mixed breed status, as well as specific breed(s).

| Variable      | Description | Possible Values |
| :--- | :---------------------------- | :------------------------------- |
| `Breed_Status`      | Owner-reported breed status       |  Mixed breed <br> Purebred |
| `Breed`      | Owner-reported single breed (if purebred) or two predominant breeds if mixed breed       |  e.g. Golden Retriever <br> St. Bernard/Australian Cattle Dog <br> Chihuahua/Unknown |

We can see that our example dog has been reported as a mixed breed, with the two breeds described:

| dog_id | Breed_Status | Breed |
| :--- | :------------------ | :-------------------- |
| 33975 | Mixed breed | Poodle/Cocker Spaniel |


#### Dog demographic reporting classifications

This section contains breed, size, weight, age, and lifestage classifications for dogs based on best practices developed by DAP researchers. Use of these classifications is recommended to promote consistency and ease of comparison among analyses. For more information regarding these classifications, see <a href="https://pubs.dogagingproject.org/node/7645" target="_blank" rel="noopener">Guidelines for reporting dog demographics</a>.

Note: a given dog's classification into some of these categories may vary over time (e.g., a female dog is spayed, a dog increases in weight as they age); all variables in the Dog Overview are calculated using a dog's status at the time of HLES completion.

| Variable      | Description | Possible Values                |
| :--- | :-------------------- | :------------------------------- |
| `Sex_Class_at_HLES`      | Owner-reported sex and sterilization status      |  Female, intact <br> Female, spayed <br> Male, neutered <br> Male, intact |
| `Weight_Class_5KGBin_at_HLES` | 5kg-increment weight bin based on owner-reported weight at HLES (for dogs estimated to be <1 year old at HLES: owner-reported expected adult weight) | e.g. 0-4.9 <br> 30-34.9 <br> 45+| 
| `Weight_Class_10KGBin_at_HLES` | 10kg-increment weight bin based on owner-reported weight at HLES (for dogs estimated to be <1 year old at HLES>: owner-reported expected adult weight) | e.g. <10 <br> 20 - 29.9 <br> 40+ | 
| `Breed_Class` | AKC status of breed(s) | AKC-Recognized Breed <br> Non-AKC-Recognized or Mixed Breed |
| `Breed_Size_Class_at_HLES` | Breed size class based on breed and owner-reported weight (for dogs estimated to be <1 year old at HLES: owner-reported expected adult weight) | Toy and small AKC-recognized purebred dogs <br> Medium AKC-recognized purebred dogs <br> Standard AKC-recognized purebred dogs <br> Large AKC-recognized purebred dogs <br> Giant AKC-recognized purebred dogs <br> Toy and small non-AKC breed dogs <br> Medium non-AKC breed dogs <br> Standard non-AKC breed dogs <br> Large non-AKC breed dogs <br> Giant non-AKC breed dogs |
| `Age_Years_Class_at_HLES` | Age bin at HLES | e.g. <1 <br> 1.0 to 2.9 <br> 9.0 to 10.9 <br> 17+ |
| `Lifestage_Class_at_HLES` |	Lifestage classification based on `Breed_Size_Class` and `Estimated_Age_at_HLES` | Puppy <br> Young adult <br> Mature adult <br> Senior |  

Our example dog is placed into the following categories:

| dog_id | Sex_Class_at_HLES | Weight_Class_5KGBin_at_HLES | Weight_Class_10KGBin_at_HLES | Breed_Class | Breed_Size_Class_at_HLES | Age_Years_Class_at_HLES | LifeStage_Class_at_HLES |
| :--- | :------------------ | :-------------------- |  :------------------- | :------------------ | :-------------------- |  :------------------- | :------------------ |
| 33975 | Male, neutered | 10-14.9 | 10-19.9 | Non-AKC-Recognized or mixed breed | Medium non-AKC and mixed breed dogs | 9-10.9 | Mature Adult |

#### Survival status

The following section provides information about the dog's survival status and related measurements:

| Variable      | Description | Possible Values | 
| :--- | :-------------------- | :------------------------------- |
| `Survival_Status` | Survival status | Alive<br>Dead | 
| `Survival_Source`<sup>1</sup> | Last point of contact with study participant; used to ascertain `Survival_Date` | 1-2-3 Treat <br> Annual Follow-Up <br> Annual Follow-Up estimated date <br> Canine Social & Learned Behavior <br> End of Life date of death <br> HLES <br> Lab Draw <br> Major events <br> Morphometrics & Mobility <br> My Profile <br> Study status date of death <br> Study Status reported date <br> Treat Hide-And-Seek <br> NA | 
| `Death_Source_Precision`<sup>1</sup> | Certainty of date of death | Actual Date<br>Estimated by Owner<br>Estimated by date provided on Major Events<br>Estimated by midpoint between AFUS & last known alive<br>NA
| `Survival_Days`<sup>1</sup> | Difference in days between `Survival_Date` and `DAP_Pack_Date`| Numeric<br>NA |
| `Survival_Date`<sup>1</sup> | Either death date or last known alive date  | YYYY-MM-DD<br>NA | 
| `Estimated_Survival_Age`<sup>1</sup> | Estimated age at `Survival_Date` | Numeric<br>NA | 

<sup>1</sup> For dogs with reported `DOD` <= `DAP_Pack_Date`, this variable is not calculated (NA).

The owner of our example dog, who has an `Estimated_DOB` of 2010-06-15 and began participating in the study on their `DAP_Pack_Date` of 2020-10-13, reported the dog's death in the End of Life Survey by providing an Actual Date. The Date of Death (`Survival_Date`) was 2025-01-21. From this, we have calculated this dog has participated in the study for 1561 Days (`Survival_Days`). At the time of Death, we estimated their age to be 14.6 years old (`Estimated_Survival_Age`). 

| dog_id | Survival_Status | Survival_Source | Death_Source_Precision | Survival_Days | Survival_Date | Estimated_Survival_Age |
| :--- | :------ | :--------- |  :------------- | :--------- |  :------ |   :------ | 
| 33975 | Dead | End of Life date of death | Actual Date | 1561 | 2025-01-21 | 14.6 |


### Survey completion

This section provides a snapshot of which surveys have been completed for a given dog.

| Variable      | Description | Possible Values |
| :--- | :---------------------------- | :------------------------------- |
| `AFUS_YearY_Complete`   | 12<sup>1</sup>-character string indicating instrument-level completion for AFUS followup year Y. Character positions indicate: <br> 1 = Owner contact <br> 2 = Dog demograpics <br> 3 = Physical activity <br> 4 = Environment <br> 5 = Behavior <br> 6 = Diet <br> 7 = Meds and Preventives <br> 8 = Health Status <br> 9 = Owner demographics <br> 10 = DORA <br> 11 = MDORS <br> 12 = Age-Related Changes<sup>1</sup> |  YYYYYYYYYYYY <br> (all instruments complete) <br><br> YYYNNNNNNNNN <br> (owner contact, dog demographics, physical activity complete) <br><br> NA <br> (dog not eligible for AFUS YearY survey)| 
| `EOLS_Complete`      | End of life survey completed    |  Y <br> NA (not reported dead) | 
| `CSLB_YYYY_Complete`      | Canine social and learned behavior completed in YYYY      |  Y <br> N <br> NA (not eligible)|
| `CognitiveGames_123Treat_YYYY_Complete`<sup>2</sup> | 123-Treat activity completed in YYYY      |  Y <br> N  <br> NA (not eligible)| 
| `CognitiveGames_TreatHideAndSeek_YYYY_Complete`<sup>3</sup> | Treat Hide & Seek completed in YYYY      |  Y <br> N  <br> NA (not eligible)|
| `MorphometricsAndMobility_YYYY_Complete`<sup>2</sup> | 3-character string indicating instrument-level completion for Morphometrics & Mobility activities in YYYY. Character positions indicate: <br> 1 = Measure Your Dog <br> 2 = Jog/Run Activity <br> 3 = Stair Climb Activity | YNN  <br> NA (not eligible)|   

<sup>1</sup> The Age-Related Changes module was deployed in 2021.  
<sup>2</sup> 1-2-3 Treat and Morphometrics and Mobility were deployed in 2022.  
<sup>3</sup> Treat Hide & Seek was deployed in 2023. 

For our example dog, all portions of AFUS except for Age-Related Changes were completed for follow-up year 1. In follow-up years 2 through 4, all 12 portions of AFUS were completed. This dog was not eligible for AFUS follow-up year 5 (NA) because the dog was reported dead prior to its annual follow-up invitation date.

| dog_id | AFUS_Year1_Complete | AFUS_Year2_Complete | AFUS_Year3_Complete | AFUS_Year4_Complete | AFUS_Year5_Complete | 
| :--- | :------ | :---- | :---- | :---- | :---- | 
| 33975 | YYYYYYYYYYYN | YYYYYYYYYYYY | YYYYYYYYYYYY | YYYYYYYYYYYY | NA | 

As we know from the survival status section, our example dog was reported dead by the owner in the End of Life Survey, and thus, the EOLS_Complete is Y.
| dog_id | EOLS_Complete |
| :--- | :------ |
| 33975 | Y | 

Looking again to our example dog, we see that the owner completed CSLB for 2020, 2021, 2022, 2023, and 2024. In 2025, the owner was not invited to complete the survey (NA) due to the dog's death earlier that year.

| dog_id | CSLB_<br>2020_Complete | CSLB_<br>2021_Complete | CSLB_<br>2022_Complete | CSLB_<br>2023_Complete | CSLB_<br>2024_Complete | CSLB_<br>2025_Complete|
| :--- | :------ | :---- | :---- | :---- | :---- | :---- |  
| 33975 | Y | Y | Y | Y | Y | NA |

The dog and owner completed the 1-2-3 Treat activity in 2022, 2023 and 2024. In 2025, the owner was not invited to complete the survey (NA) due to the dog's death earlier that year. 

| dog_id | CognitiveGames_123Treat_<br>2022_Complete | CognitiveGames_123Treat_<br>2023_Complete | CognitiveGames_123Treat_<br>2024_Complete | CognitiveGames_123Treat_<br>2025_Complete |  
| :--- | :------ | :---- | :---- | :---- |
| 33975 | Y | Y | Y | NA |

The dog and owner completed Treat Hide & Seek in both 2023 and 2024. In 2025, the owner was not invited to complete the survey (NA) due to the dog's death earlier that year.

| dog_id | CognitiveGames_<br>TreatHideAndSeek_<br>2023_Complete | CognitiveGames_<br>TreatHideAndSeek_<br>2024_Complete | CognitiveGames_<br>TreatHideAndSeek_<br>2025_Complete |
| :--- | :------ | :---- |  :---- |  
| 33975 | Y | Y | NA |

The dog and owner completed all three of the Morphometrics and Mobility activities in 2022, two of the three Morphometrics and Mobility activities in 2023, and none in 2024. In 2025, the owner was not invited to complete the survey (NA) due to the dog's death earlier that year.

| dog_id | MorphometricsAndMobility_<br>2022_Complete | MorphometricsAndMobility_<br>2023_Complete | MorphometricsAndMobility_<br>2024_Complete | MorphometricsAndMobility_<br>2025_Complete |
| :--- | :------ | :---- | :---- | :---- |
| 33975 | YYY | YYN | NNN | NA |

### DNA Kit

For dogs enrolled in Foundation and Precision, a DNA sample is submitted for sequencing. If sequencing data for a given dog was returned from the lab by December 31st of the Data Release Year, the `DNA_Swab_ID` is provided. This variable can be used to link to genetic sequence data in the corresponding release year, see <a href="https://github.com/dogagingproject/dataRelease/blob/master/Supporting_Documents/DAP_GeneticData_UserGuide.md" target="_blank" rel="noopener">Genetic Data User Guide</a>.  

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `DNA_Swab_ID`      | Swab ID     |  31020061515058 |

The example dog is enrolled in Precision, and we see a `DNA_Swab_ID` populated.

| dog_id       | DNA_Swab_ID |
| :--- | :---------------------------- |
| 33975  |  31020061515291 |


<!--### Environment data 

Owner-reported primary and secondary addresses are geocoded and linked to secondary data describing characteristics of the dog's environment. The following variables provide information about availabilty of environmental data for a given dog:

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `PrimaryAddress_HLES`      | Participant has primary address at HLES geocoded and linked to environmental data      |  Y <br> N |
| `SecondaryAddress_HLES`      | Participant has secondary address at HLES geocoded and linked to environmental data     |  Y <br> N  |

These fields indicate the presence of a geocoded primary address provided at HLES, but no geocoded secondary address for our example dog.

| dog_id      | PrimaryAddress_HLES | SecondaryAddress_HLES | 
| :--- | :---------------------------- | :------------------------------- |
| 33975   | Y | N | 
-->
*** 

###### *last updated 2026-02-13*
