## Dog Aging Project | Dog Aging Project | Morphometrics & Mobility User Guide

### Overview

This document provides an introduction to the Morphometrics & Mobility dataset. These data are collected through a series of at-home activities presented as the Measurement & Mobility Activities to dogs in the DAP Pack annually. These activities take 45-60 minutes to complete in total. Owners are guided through a series of REDCap instruments, which include:
- Measuring Your Dog
- Jog & Run Activity
- Stair Climb Activity 

Successful completion of these activities by the participant requires access to specific materials and appropriate space and locations. Participants can opt-in or opt-out of any or all of the tasks; as a result, existing data may only reflect some/all activities for a given dog in a given year. Each activity is contained in a standalone dataset.

[Materials List for Measurement & Mobility Activities (PDF)](ReferenceFiles/Materials%20List%20for%20Measurement%20&%20Mobility%20Activities.pdf)

### Morphometrics & Mobility: Measuring Your Dog

This instrument explains to participants how to take a series of body measurements on their dog. Participants can measure in centimeters or inches. If they measure in centimeters, they are instructed to round to the nearest 0.5 cm. If they measure in inches, they are instructed to round to the nearest 0.25 in. All data in the Morphometrics & Mobility dataset are reported in centimeters. 

- [Measuring Your Dog Instructions & Data Sheet (PDF)](ReferenceFiles/Measure%20Your%20Dog_Instructions%20&%20Data%20Sheet.pdf)
- [Measuring Your Dog Video Instructions (Vimeo)](https://vimeo.com/685622195)

The following data are provided to identify an instance of Morphometrics & Mobility: Measuring Your Dog data collection.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `dog_id`      | Unique dog identifier       | Integer | 
| `survey_year` | Study year | annual_YYYY |
| `mm_myd_date` | Date Measure Your Dog Activity was completed | YYYY-MM-DD |

The following data are collected via the Measuring Your Dog instrument:

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `mm_myd_recent_dog_weight_kg`      | Most recent dog weight in kg       | numeric | 
| `mm_myd_recent_dog_weight_month` | Month of most recent dog weight | Integer |
| `mm_myd_recent_dog_weight_year` | Year of most recent dog weight | Integer |
| `mm_recent_dog_weight_location` | Where most recent dog weight was measured | 1 (Veterinarian’s office)<br> 2 (Pet store)<br> 3 (At home)<br> 98 (Other) |
| `mm_myd_head_length_cm` | Dog’s head length in cm | Numeric |
| `mm_myd_head_circumference_cm` | Dog’s head circumference in cm | Numeric |
| `mm_myd_shoulder_height_cm` | Dog’s shoulder height in cm | Numeric |
| `mm_myd_shoulder_measured_side` | Side of body dog’s shoulder measurement was taken from | 1 (Left)<br>2 (Right) |
| `mm_myd_back_length_cm` | Dog’s back length in cm | Numeric | 
| `mm_myd_body_circumference_cm` | Dog’s body circumference | Numeric |
| `mm_myd_front_leg_length_cm` | Dog’s front leg length in cm | Numeric | 
| `mm_myd_front_leg_measured_side` | Side of body dog’s front leg length measurement was taken from | 1 (Left)<br>2 (Right) |
| `mm_myd_rear_left_circumference_cm` | Circumference of dog’s rear left leg in cm <sup>1</sup> | Numeric | 
| `mm_myd_rear_right_leg_circumference_cm` | Circumference of dog’s rear right leg in cm<sup>1</sup>| Numeric |

<sup>1</sup>Owners were instructed to enter “NA” if dog is missing leg

### Morphometrics & Mobility: Jog & Run Activity

This instrument guides participants through setting up 10-meter course, which they use to conduct three repetitions of the jogging activity and three repetitions of the running activity.

- [Jog & Run Activity Instructions & Data Sheet (PDF)](ReferenceFiles/Jog%20&%20Run%20Activity_Instructions%20&%20Data%20Sheet.pdf)
- [How to Set Up the 10-Meter Course Demonstration Video (Vimeo)](https://vimeo.com/685613159)
- [Timed 10-Meter Jog Demonstration Video (Vimeo)](https://vimeo.com/684839241)
- [Timed 10-Meter Run Demonstration Video (Vimeo)](https://vimeo.com/684839751)

The following data are provided to identify an instance of Morphometrics & Mobility: Jog & Run Activity data collection.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `dog_id`      | Unique dog identifier       | 12345 | 
| `survey_year` | Study year | annual_YYYY |
| `mm_jr_date` | Date Jog/Run Activity was completed | YYYY-MM-DD |

The following data are collected via the Jog & Run Activity instrument:

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `mm_jr_location` | Location has been previously used by owner for jog/run activity | 0 (No)<br>1 Yes)  | 
| `mm_jr_location_description` | Description of jog/run activity location | Text  | 
| `mm_jr_practice_jog_trials` | Number of jog practice trials | 1<br>2<br>3<br>4<br>5  | 
| `mm_jr_jog_trial_*_outcome` | Dog successfully completed course in jog trial * | 0 (No)<br>1 Yes)  | 
| `mm_jr_jog_trial_*_time_seconds` | Time for dog to jog from start to finish in seconds in jog trial * | Numeric  | 
| `mm_jr_jog_trial_*_problems` | Problems encountered in jog trial * | Text  | 
| `mm_jr_jog_trials_motivation_*` | Motivator used during jog trials | 0 (No)<br>Yes(1)  | 
| `mm_jr_jog_trials_motivation_other_description` | Description of other motivator used during jog trials | Text  | 
| `mm_jr_number_practice_run_trials` | Number of practice run trials | 1<br>2<br>3<br>4<br>5  | 
| `mm_jr_run_trial_*_outcome` | Dog successfully completed course in run trial * | 0 (No)<br>1 Yes)  | 
| `mm_jr_run_trial_*_time_seconds` | Time for dog to run from start to finish in seconds in run trial * | Numeric  | 
| `mm_jr_run_trial_*_problems` | Problems encountered in run trial * | Text  | 
| `mm_jr_jog_trials_motivation_*` | Motivator used during run trials | 0 (No)<br>Yes (1)  | 
| `mm_jr_jog_trials_motivation_other_description` | Description of other motivator used during jog trials | Text  | 

### Morphometrics & Mobility: Stair Climb Activity

This instrument guides participants through an activity in which they time their dog running up a safe flight of stairs through three repetitions. 

- [Stair Climb Activity Instructions (PDF)](ReferenceFiles/Stair%20Climb%20Activity_Instructions%20&%20Data%20Sheet.pdf)
- [Counting and Measuring Stairs Demonstration Video (Vimeo)](https://vimeo.com/685616417)
- [Timed Stair Climb Demonstration Video (Vimeo)](https://vimeo.com/685615694)

The following data are provided to identify an instance of Morphometrics & Mobility: Stair Climb Activity data collection.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `dog_id`      | Unique dog identifier       | 12345 | 
| `survey_year` | Study year | annual_YYYY |
| `mm_sc_date` | Date Stair Climb Activity was completed | YYYY-MM-DD |

The following data are collected via the Stair Climb Activity instrument:

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `mm_sc_stairs_used_previously` | Location has been previously used by owner for stair climb activity | 0 (No)<br> 1 (Yes)  | 
| `mm_sc_loc_y` | Flooring surface of stairs has changed since last used for stair climb activity | 0 (No)<br> 1 (Yes)  | 
| `mm_sc_stairs_used_description` | Description of stairs | Text  | 
| `mm_sc_stair_height_cm` | Height of second stair in cm | Numeric  | 
| `mm_sc_stair_count` | Number of stairs | Integer  | 
| `mm_sc_number_practice_trials` | Number of practice stair climb trials | 1<br>2<br>3<br>4<br>5  | 
| `mm_sc_trial_*_outcome` | Dog successfully completed course in stair climb trial * | 0 (No)<br>1 (Yes)  | 
| `mm_sc_trial_*_time_seconds` | Time for dog to run up stairs in seconds in stair climb trial * | Numeric  | 
| `mm_sc_trial_*_problems` | Problems encountered in stair climb trial * | Text  | 
| `mm_sc_trials_motivation_*` | Motivator used during stair climb trials | 0 (No) <br>1 (Yes) | 
| `mm_sc_trials_motivation_other_description` | Description of other motivator used during stair climb trials | Text  | 


*** 

###### *last updated 2024-01-31*