Each viewable table requires a primary key or identifier column for display purposes.
These columns are not contained in the downloadable data files.

These columns are constructed in the following manner:

| TableName      | Primary key construction |
| :--- | :----------- |
| HLES_dog_owner      | [dog_id]       |
| HLES_cancer_conditions   | [dog_id]        |
| HLES_health_conditions   | [dog_id]_*[hs_condition_type]*_[hs_condition]_*instance*       |
| AFUS_dog_owner   | [dog_id]_[afus_calendar_year]        |
| AFUS_cancer_conditions   | [dog_id]_*[afus_calendar_year]*_*instance*       |
| AFUS_health_conditions | [dog_id]_*[afus_calendar_year]*_[afus_hs_new_condition_type]_*[afus_hs_new_condition]*_*instance*        |
| CSLB   | [dog_id]_[cslb_year] |
| EOLS  | [dog_id]     |

