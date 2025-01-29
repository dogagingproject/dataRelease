## Dog Aging Project | Treat Hide & Seek User Guide

### Overview

Treat Hide & Seek is a spatial memory task that assesses a dog’s recall of the location of a food reward over longer and longer intervals. A schematic of the task setup is provided in Figure 1 (below).

The activity begins with a series of warm-ups in which the dog is introduced to the process of searching for treats in small boxes, positioned at two locations as indicated in Figure 1. Following this warm-up, the dog participates in a series of sixteen trials assessing spatial memory. On each trial, the dog and handler begin at a location equidistant from the two boxes where rewards will be placed (start location in Figure 1). A helper sits five feet away as indicated by the purple square in Figure 1. The helper places a treat in one of the two boxes. The dog is allowed to observe the baiting process. After a set amount of time, the handler releases the dog to search for the treat. 

- Delay for trials 1-4: 0 seconds 
- Delay for trials 5-8:	10 seconds 
- Delay for trials 9-12: 20 seconds 
- Delay for trials 13-16:	40 seconds 

After each trial, the dog is returned to the start position. The order in which the boxes are baited is counterbalanced across trials (occurring eight times at each location, following a predetermined order).

__Figure 1. Schematic of the physical setup for Treat Hide & Seek.__<br>
![Figure 1](ReferenceFiles/THAS_Fig1.JPG)

### About This Document 

This document provides an introduction to the Treat Hide & Seek dataset. Treat Hide & Seek is an at-home cognitive assessment presented to dogs in the DAP Pack annually. Owners are guided through the Treat Hide & Seek Activity in their personal research portal using a combination of written and video instructions.  
- [Treat Hide & Seek Overview (Video)](https://vimeo.com/842997796/97d082dc00?share=copy)
- [Treat Hide & Seek Box Construction Instructions (PDF)](ReferenceFiles/Cognitive_Treat_Hide_and_Seek_Box_Construction_Instructions_THS.pdf)
- [Treat Hide & Seek Activity Instructions (PDF)](ReferenceFiles/Cognitive_Treat_Hide_and_Seek_Activity_Instructions.)

The following data are provided to identify an instance of Treat Hide & Seek data collection.

| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `dog_id`      | Unique dog identifier       | Integer | 
| `survey_year` | Study year | annual_YYYY |
| `ths_game_date` | Date of Treat Hide & Seek completion | YYYY-MM-DD |

The following data are collected via the Treat Hide & Seek instrument:
| Variable      | Description | Example Values |
| :--- | :---------------------------- | :------------------------------- |
| `ths_hand_feed_response`      | Dog response to offered treat | 1 (Did not eat)<br>2 (Reluctant)<br>3 (Enthusiastic) | 
| `ths_box_feed_response` | Dog response to offered treat | 1 (Did not eat)<br>2 (Reluctant)<br>3 (Enthusiastic) | 
| `ths_warmup_*_location` | Treat location on warmup round * | 1 (Box 1)<br>2 (Box 2) |
| `ths_warmup_*_response` | Dog's response on warmup round * | 0 (No)<br>1 (Yes)<br>6 (Stopped activity) |
| `ths_game_*_location` | Treat location on game round * | 1 (Box 1) <br> 2 (Box 2) |
| `ths_game_*_response` | Dog's response on game round * | 1 (Searched in Box 1 first)<br>2 (Searched in Box 2 first)<br>4 (Didn't search in any box)<br>5 (Something went wrong)<br>6 (My dog is not enjoying this activity, and we need to stop) |
| `ths_game_feedback` | Experience with activity | Text | 
| `ths_game_optout_reason` | Owner opt-out reason | 1 (My dog is not interested in the treats anymore)<br>2 (My dog is tired)<br>3 (My dog is distracted)<br>4 (We don't have time to complete this)<br>98 (Other) | 
| `ths_food_motivation` | Dog's enthusiasm for finding treats | 1 (Not excited)<br>2 (Moderately excited)<br>3 (Very excited) | 
| `ths_previous_scentwork` | Dog trained in scentwork or nosework | 0 (No)<br>1 (Yes) |
| `ths_location` | Description of activity space | 1 (Indoor space)<br>2 (Fenced yard)<br>3 (Unfenced yard)<br>4 (Public park)<br>98 (Other) |  

### Example R code

This code provides an example of how to calculate summary scores for the Dog Aging Project Treat Hide & Seek Activity.

`library(tidyverse); theme_set(theme_bw(18))`<br>
`library(haven)`

`dat <- read_csv("data/DAP_YYYY_CognitiveGames_TreatHideAndSeek_v1.0.csv")`<br>

`# format date column`<br>
`dat <- dat |> mutate(ths_game_date = mdy(ths_game_date))`<br>

`# make data frame with correct location by trial`<br>
`cor_locs <- dat |>
  select(contains("ths_game_round") & ends_with("location")) |>
  unique() |>
  pivot_longer(cols = everything()) |>
  mutate(trial = str_remove(name, "ths_game_round") |>
    str_remove("_location") |> as.numeric()) |>
  select(-name, cor_loc = value)`<br>

`# data frame with responses during game rounds`<br>
`trials <- dat |> select(dog_id, survey_year, ths_game_date, contains("ths_game_round") & contains("response"))`<br>

`# make longer`<br>
`trials <- trials |> pivot_longer(cols = contains("ths_game_round"))`<br>

`# extract trial number from string`<br>
`trials <- trials |>
  mutate(trial = str_remove(
    name, "ths_game_round") |> 
      str_remove("_response") |> 
      as.numeric()) |>
  select(-name, response = value)`<br>

`# join trial-level responses with data frame of correct locations`<br>
`df <- full_join(trials, cor_locs)`<br>

`rm(trials, dat, cor_locs)`<br>

`# add delay durations`<br>
`df <- df |> mutate(delay = case_when(
  trial > 0 & trial < 5 ~ "0",
  trial > 4 & trial < 9 ~ "10",
  trial > 8 & trial < 13 ~ "20",
  trial > 12 ~ "40",
))`<br>

`# relocate columns for more intuitive organization`<br>
`df <- df |>
  relocate(delay, .after = trial) |>
  relocate(response, .after = cor_loc)`<br>

`# add variable reflecting whether dog's search was to correct location`<br>
`df <- df |> mutate(correct = if_else(response == cor_loc, true = 1, false = 0))`<br>

`# calculate summary scores by delay length`<br>
`delay_summary <- df |>
  group_by(dog_id, survey_year, ths_game_date, delay) |>
  summarise(prop_correct = mean(correct, na.rm = T), n_trials = n())`<br>

`# add birth dates from dog overview`<br>
`load("data/DAP_YYYY_DogOverview_v1.0.RData")`<br>

`# extract dog id and birth date`<br>
`DogOverview <- DogOverview |>
  select(dog_id, Estimated_DOB) |>
  zap_labels() |>
  zap_label() |>
  mutate(dob = ymd(Estimated_DOB))`<br>

`# join with treat hide and seek summary`<br>
`delay_summary <- left_join(delay_summary, select(DogOverview, dog_id, dob))`<br>

`# calculate age on date treat hide and seek was played`<br>
`delay_summary <- delay_summary |> mutate(age_at_test = interval(dob, ths_game_date) / years(1))`<br>

`# plot mean performance by age`<br>
`ggplot(filter(delay_summary, age_at_test < 16), aes(x = age_at_test, y = prop_correct)) +
  stat_summary_bin(breaks = seq(0, 15, 3)) +
  facet_grid(cols = vars(delay)) +
  labs(x = "age (years)", y = "proportion correct responses")`<br>

![Figure 2](ReferenceFiles/THAS_x_age.jpeg)
*** 

###### *last updated 2025-01-24*