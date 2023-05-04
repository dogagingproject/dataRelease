## Dog Aging Project | Dog Overview User Guide

This document provides an introduction to the Dog Overview dataset using an example dog from the 2021 Curated Data release.

### Dog status

This section provides basic information about the dog, including its unique identifier, when the dog became a member of the DAP Pack, and details about the dog's enrollment in a cohort (if relevant).

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `dog_id`      | Unique dog identifier       | 12345 | 
| `DAP_Pack_Date` | Date of HLES completion | YYYY-MM-DD |
| `Cohort` | Dog's enrolled cohort, if any | DAP Pack <br> Foundation <br>  Precision |
| `Cohort_Enroll_Date` | Date enrolled in Foundation or Precision Cohort (if applicable) | YYYY-MM-DD |

Using `dog_id` 33975 as an example, we can see that the dog became a member of the DAP pack on 2020-10-13, and was enrolled in the Precision cohort on 2021-06-21.

| dog_id | DAP_Pack_Date | Cohort | Cohort_Enroll_Date |
| :--- | :------------------ | :-------------------- |  :------------------- |
| 33975 | 2020-10-13 | Precision | 2021-06-01 |


### Dog demographics

This section provides details regarding  basic characteristics of a given dog, such as date of birth, sex, breed, and date of death (if relevant), as well as dog demographic reporting classifications (see relevant section for details).

#### Estimated age and DOB, DOD

In HLES, owners are asked to provide their dog's birth year (and month, if known), or, at the very least, their dog's age. Using that information along with the date of HLES completion, a dog's DOB and age at HLES can be estimated by the following methods.

| Owner provided      | DOB estimation method | Age estimation method |
| :--- | :---------------------------- | :------------------------------- |
| Birth year and month | Use birth year and month; assume 15 for day | Difference between estimated DOB and HLES completion date |
| Birth year only | Use birth year; if birth year != HLES completion year, assume 6 for month and 15 for day; otherwise assume midpoint between 1/1 and HLES completion date | Difference between estimated DOB and HLES completion date |
| Age | Substract age from HLES completion date | Use owner-reported age | 

These estimation methods are used to define the following variables.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `Estimated_DOB`      | Best available estimate of DOB at HLES       | YYYY-MM-DD |
| `Estimated_Age_Years_at_HLES` | Best available estimate of age at HLES | 3.5 |
| `AgeDOB_Estimation_Method` | Method used to estimate DOB and age |  Estimated using owner-reported age <br> Estimated using owner-reported birth year <br> Estimated using owner-reported birth year and month |

Going back to our example dog, we see that age and DOB were estimated using owner-provided birth year only. The owner indicated that the dog was born in 2010. The birth year and year of HLES completion are different, so we assume the birth month to be June and the birth day to be the 15th, resulting in an estimated DOB of 2010-06-15. If we subtract the estimated DOB from the date of HLES completion (which is the same as the DAP Pack date), we estimate the dog's age at HLES to be 10.3 years. 

| dog_id      | DAP_Pack_Date | Estimated_DOB | Estimated_Age_Years_at_HLES | AgeDOB_Estimation_Method | 
| :--- | :------------------ | :-------------------- |  :------------------- | :------------ |
| 33975 | 2020-10-13 | 2010-06-15 | 10.3 | Estimated using owner-reported birth year | 


The following section provides information about the dog's death, if applicable. 

| Variable      | Description | Example Values | 
| :--- | :---------------------------- | :------------------------------- |
| `Dog_Reported_Deceased` | Owner has notified DAP of dog's death by any method  | Y <br> N | 
| `DOD` | Owner-reported date of dog's death from EOLS  | YYYY-MM-DD | 

At the time of this writing, our example dog has not been reported as deceased, so no `DOD` exists.

| dog_id | Dog_Reported_Deceased | DOD |
| :--- | :------------------ | :-------------------- |
| 33975 | N | NA |

#### Dog breed(s)

This section provides information regarding purebred or mixed breed status, as well as specific breed(s).

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `Breed_Status`      | Owner-reported breed status       |  Mixed breed <br> Purebred |
| `Breed`      | Single breed (if purebred) or two predominant breeds if mixed breed       |  Golden Retriever <br> St. Bernard/Australian Cattle Dog <br> Chihuahua/Unknown |

We can see that our example dog has been reported as a mixed breed, with the two breeds described:

| dog_id | Breed_Status | Breed |
| :--- | :------------------ | :-------------------- |
| 33975 | Mixed breed | Poodle/Cocker Spaniel |


#### Dog demographic reporting classifications

This section contains breed, size, weight, age, and lifestage classifications for dogs based on best practices developed by DAP. Use of these classifications is recommended to promote consistency and ease of comparison among analyses. For more information regarding these classifications, see [Guidelines for reporting dog demographics](https://pubs.dogagingproject.org/node/7645). Note: a given dog's classification into some of these categories may vary over time (e.g., a female dog is spayed, a dog increases in weight as they age); all variables in the Dog Overview are calculated using a dog's status at the time of HLES completion.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `Sex_Class_at_HLES`      | Owner-reported sex and sterilization status      |  Female, intact <br> Female, spayed <br> Male, neutered <br> Male, intact |
| `Weight_Class_at_HLES_5kg` | 5kg-increment weight bin at HLES | 0-4.9 <br> 30-34.9 <br> 45+| 
| `Weight_Class_at_HLES_10kg` | 10kg-increment weight bin at HLES | <10 <br> 20 - 29.9 <br> 40+ | 
| `Breed_Class` | AKC status of breed(s) | AKC-Recognized Breed <br> Non-AKC-Recognized or Mixed Breed |
| `Breed_Size_Class` | Breed size class based on breed and weight | Toy and small AKC-recognized purebred dogs <br> Medium AKC-recognized purebred dogs <br> Standard AKC-recognized purebred dogs <br> Large AKC-recognized purebred dogs <br> Giant AKC-recognized purebred dogs <br> Toy and small non-AKC breed dogs <br> Standard non-AKC breed dogs <br> Large non-AKC breed dogs <br> Giant non-AKC breed dogs |
| `Age_Class_at_HLES` | Age bin at HLES | <1 <br> 1.0 to 2.9 <br> 9.0 to 10.9 <br> 17+ |
| `Lifestage_Class_at_HLES` |	Lifestage classification based on `Breed_Size_Class` and `Estimated_Age_at_HLES` | Puppy <br> Young adult <br> Mature adult <br> Senior |

Our example dog is placed into the following categories:

| dog_id | Sex_Class_at_HLES | Weight_Class_5KGBin_at_HLES | Weight_Class_10KGBin_at_HLES | Breed_Class | Breed_Size_Class_at_HLES | Age_Years_Class_at_HLES | LifeStage_Class_at_HLES |
| :--- | :------------------ | :-------------------- |  :------------------- | :------------------ | :-------------------- |  :------------------- | :------------------ |
| 33975 | Male, neutered | 10-14.9 | 10-19.9 | Non-AKC-Recognized or mixed breed | Medium non-AKC and mixed breed dogs | 9-10.9 | Mature Adult |


### Survey completion

This section provides a snapshot of which surveys have been completed for a given dog.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `CSLB_YYYY_Complete`      | Canine social and learned behavior completed in YYYY      |  Y <br> N |
| `AFUS_YYYY_Complete`*      | 11-character string indicating instrument-level completion for AFUS YYYY. Character positions indicate: <br> 1 = Owner contact <br> 2 = Dog demograpics <br> 3 = Physical activity <br> 4 = Environment <br> 5 = Behavior <br> 6 = Diet <br> 7 = Meds and Preventives <br> 8 = Health Status <br> 9 = Owner demographics <br> 10 = DORA <br> 11 = MDORS |  YYYYYYYYYYY <br> (all instruments complete) <br><br> YYYNNNNNNNN <br> (owner contact, dog demographics, physical activity complete) | 
| `AFUS_YearY_Complete`*      | 11-character string indicating instrument-level completion for AFUS followup year Y. Character positions indicate: <br> 1 = Owner contact <br> 2 = Dog demograpics <br> 3 = Physical activity <br> 4 = Environment <br> 5 = Behavior <br> 6 = Diet <br> 7 = Meds and Preventives <br> 8 = Health Status <br> 9 = Owner demographics <br> 10 = DORA <br> 11 = MDORS |  YYYYYYYYYYY <br> (all instruments complete) <br><br> YYYNNNNNNNN <br> (owner contact, dog demographics, physical activity complete) | 
| `EOLS_Complete`      | End of life survey complete    |  Y <br> N | 
*`AFUS_YYYY_Complete` replaced by `AFUS_YearY_Complete` beginning in 2022 Curated Data release.

Looking again to our example dog, we see that the owner completed CSLB for both 2020 and 2021. All portions of AFUS were completed for 2021. And (unsurprisingly, since we have no knowledge of the dog being deceased), EOLS has not been completed.

| dog_id | CSLB_2020_Complete | CSLB_2021_Complete | AFUS_2021_Complete | EOLS_Complete |
| :--- | :------------------ | :-------------------- | :------------------ | :-------------------- |
| 33975 | Y | Y | YYYYYYYYYYY | N | 


### DNA Kit

For dogs enrolled in Foundation and Precision, a DNA sample is submitted for sequencing. If sequencing data for a given dog was returned from lab by 2021-12-31, the `DNA_Swab_ID` is provided.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `DNA_Swab_ID`      | Swab ID     |  31020061515058 |

The example dog is enrolled in Precision, and we see a `DNA_Swab_ID` populated, indicating that sequencing results were returned by 2021-12-31.

| dog_id       | Example Values |
| :--- | :---------------------------- |
| 33975  |  31020061515058 |


### Clinical Lab Data (first available for Open Access in 2022 Curated Data Release)

Blood and urine samples are collected from dogs enrolled in the Precision cohort. Any laboratory results returned by DataYear-12-31 are included in the Curated data. The following variables provide information about a given dog's clinical lab data status:

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `Sample_Y1_CBC`      | CBC results available     |  Y <br> N |
| `Sample_Y1_CP`      | Blood chemistry panel results available    |  Y <br> N  |
| `Sample_Y1_UA`      | Urinalysis results available   |  Y <br> N  |

The example dog is enrolled in Precision, and CBC, CP, and UA results were returned by DataYear-12-31. This indicates that sample data results are expected in the Clinical Lab Data files.

| dog_id      | Sample_Y1_CBC | Sample_Y1_CP | Sample_Y1_UA
| :--- | :---------------------------- | :------------------------------- | :------------------------------- |
| 33975      | Y    |  Y | Y |
 

### Environment data 

Owner-reported primary and secondary addresses are geocoded and linked to secondary data describing characteristics of the dog's environment. The following variables provide information about availabilty of environmental data for a given dog:

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `PrimaryAddress_HLES`      | Participant has primary address at HLES geocoded and linked to environmental data      |  Y <br> N |
| `SecondaryAddress_HLES`      | Participant has secondary address at HLES geocoded and linked to environmental data     |  Y <br> N  |

These fields indicate the presence of a geocoded primary address provided at HLES, but no geocoded secondary address for our example dog.
Additionally, the participant did not provide any updated primary or secondary address information in their 2021 AFUS responses. 

| dog_id      | PrimaryAddress_HLES | SecondaryAddress_HLES | PrimaryAddress_AFUS2021 | SecondaryAddress_AFUS2021 |
| :--- | :---------------------------- | :------------------------------- | :---------------------------- | :------------------------------- |
| 33975   | Y | N | N | N |

*** 

###### *last updated 2023-05-04*