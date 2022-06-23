### Dog Aging Project | Known data issues

***
  
**Affected Dataset: HLES_health_conditions**

**Affected Variable(s): hs_diagnosis_year, hs_initial_diagnosis_year**

We have identified two issues with these year variables:
* (1) There are instances where the respondent inputted values for the diagnosed year of a health/cancer condition that are outside of the valid range of 1980-2025 allowed by REDCap (e.g., "07").
* (2) There are instances where the diagnosis year of a health/cancer condition is before the birth year of the dog.

For both issues, please see [DAP_Yearvariables](https://github.com/dogagingproject/dataRelease/blob/master/Supporting_Documents/DAP_Yearvariables.pdf) for more details and examples in the data. We have not modified these year variables and are leaving it up to the researcher to address and correct these records as they see fit.

***

**Affected Dataset: HLES_health_conditions**

**Affected Variable(s): hs_condition_type, hs_condition**

In the Health Status form, a participant is first asked if their dog has ever been diagnosed
with a condition of type X (e.g., eye condition) in a Yes or No type question. These “condition
type” gating questions are all required to be answered. For each condition type that the
participant indicates “Yes”, they are then presented with a set of possible specific conditions
(e.g., blindness, cataracts, etc. for the eye condition type). However, these questions asking
about specific conditions are NOT required to be answered. As a result, rows exist in the HLES
`DAP_[year]_HLES_health_conditions_[datasetVersion].***` that have values for only the following three columns: dog_id,
hs_condition_type, and hs_condition_is_congenital. As a result, these rows would have missing
values for the other 9 columns in `DAP_[year]_HLES_health_conditions_[datasetVersion].***`: hs_condition,
hs_condition_cause_other_description, hs_condition_other_description, hs_diagnosis_month,
hs_diagnosis_year, hs_eye_condition_cause, hs_follow_up_ongoing,
hs_neurological_condition_vestibular_disease_type, and hs_required_surgery_or_hospitalization.

***

**Affected Dataset: AFUS_health_conditions**

**Affected Variable(s): afus_hs_new_condition_type, afus_hs_new_condition**

In the Follow-up Health Status form, a participant is first asked if their dog has ever been diagnosed
with a condition of type X (e.g., eye condition) in a Yes or No type question. These “condition
type” gating questions are all required to be answered. For each condition type that the
participant indicates “Yes”, they are then presented with a set of possible specific conditions
(e.g., blindness, cataracts, etc. for the eye condition type). However, these questions asking
about specific conditions are NOT required to be answered. As a result, rows exist in the HLES
`DAP_[year]_AFUS_health_conditions_[datasetVersion].***` that have values for only the following three columns: dog_id,
hs_condition_type, and hs_condition_is_congenital. As a result, these rows would have missing
values for the other 9 columns in `DAP_[year]_AFUS_health_conditions_[datasetVersion].***`: afus_hs_new_condition,
afus_hs_new_condition_cause_other_description, afus_hs_new_condition_other_description, afus_hs_new_diagnosis_month,
afus_hs_new_diagnosis_year, afus_hs_new_eye_condition_cause, afus_hs_new_follow_up_ongoing,
afus_hs_new_neurological_condition_vestibular_disease_type, and afus_hs_new_required_surgery_or_hospitalization.

***

**Affected Dataset: CSLB**

**Affected Variable(s): all**

Some participants indicated that their dogs both “never” displays any behaviors/actions that would indicate toward cognitive dysfunction, yet are displaying all of the behaviors/actions “much less” compared to six months ago. We recommend removing responses with cslb_score less than 20 prior to analysis. Removing dogs with cslb_score <20 will likely remove samples in a biased manner: dogs without canine cognitive dysfunction (cslb_score < 50) are more likely to be the ones with erroneously low scores. However, most dogs in the sample have scores less than 50 and the number removed is small compared to the 20,000+ dogs in the total sample.

***

###### *last updated 2022-06-22*