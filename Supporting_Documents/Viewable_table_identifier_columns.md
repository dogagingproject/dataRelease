Each viewable table requires a primary key or identifier column for display purposes.
These columns are not contained in the downloadable data files.

These columns are constructed in the following manner:

| TableName      | Primary key construction |
| :--- | :----------- |
| HLES_dog_owner      | [dog_id]       |
| HLES_cancer_conditions   | [dog_id]        |
| HLES_health_conditions   | [dog_id]__[hs_condition_type]__[hs_condition]__*instance*       |
| AFUS_dog_owner   | [dog_id]_[afus_calendar_year]        |
| AFUS_cancer_conditions   | [dog_id]__[afus_calendar_year]__*instance*       |
| AFUS_health_conditions | [dog_id]__[afus_calendar_year]__[afus_hs_new_condition_type]__[afus_hs_new_condition]__*instance*        |
| CSLB   | [dog_id]_[cslb_year] |
| EOLS  | [dog_id]     |

