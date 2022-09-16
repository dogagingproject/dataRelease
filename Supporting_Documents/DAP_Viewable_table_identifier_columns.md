### Dog Aging Project | Viewable table identifier column descriptions

Each viewable table requires a primary key or identifier column for display purposes.
These columns are not contained in the downloadable data files.

These columns are constructed in the following manner:

| TableName      | Primary key construction |
| :--- | :----------- |
| DogOverview      | `[dog_id]`       |
| HLES_dog_owner      | `[dog_id]`       |
| HLES_cancer_conditions   | `[dog_id]`        |
| HLES_health_conditions   | `[dog_id]_[hs_condition_type]_[hs_condition]_instance`     |
| AFUS_dog_owner   | `[dog_id]_[afus_calendar_year]`   |
| AFUS_cancer_conditions   | `[dog_id]_[afus_calendar_year]_instance`       |
| AFUS_health_conditions | `[dog_id]_[afus_calendar_year]_[afus_hs_new_condition_type]_[afus_hs_new_condition]_instance`       |
| CSLB   | `[dog_id]_[cslb_year]` |
| EOLS  | `[dog_id]`    |
| ClinicalLabData      | `[dog_id]_[Year]`       |

*** 

###### *last updated 2022-09-16*