This document provides further description of known data issues.

<hr>
  
**Affected Dataset: HLES_health_conditions**
**Affected Variable(s): hs_diagnosis_year, hs_initial_diagnosis_year**
We have identified two issues with these year variables:
* (1) There are instances where the respondent inputted values for the diagnosed year of a health/cancer condition that are outside of the valid range of 1980-2025 allowed by REDCap (e.g., "07").
* (2) There are instances where the diagnosis year of a health/cancer condition is before the birth year of the dog.

For both issues, please see [DAP_Yearvariables](https://github.com/dogagingproject/dataRelease/blob/master/Supporting_Documents/DAP_Yearvariables.pdf) for more details and examples in the data. We have not modified these year variables and are leaving it up to the researcher to address and correct these records as they see fit.

<hr>

**Affected Dataset: CSLB**
**Affected Variable(s): all**
Some participants indicated that their dogs both “never” displays any behaviors/actions that would indicate toward cognitive dysfunction, yet are displaying all of the behaviors/actions “much less” compared to six months ago. We recommend removing responses with cslb_score less than 20 prior to analysis. Removing dogs with cslb_score <20 will likely remove samples in a biased manner: dogs without canine cognitive dysfunction (cslb_score < 50) are more likely to be the ones with erroneously low scores. However, most dogs in the sample have scores less than 50 and the number removed is small compared to the 20,000+ dogs in the total sample.