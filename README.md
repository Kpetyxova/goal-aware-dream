# Goal-Aware DeepPavlov DREAM

This is a Goal-Aware verson of DeepPavlov Dream Socialbot, which was developed as part of
bachelor thesis "Goal Tracker and Dialogue Games for Low-Level Human Goals in Open-Domain Conversations"[https://drive.google.com/file/d/1ODTDJwNNaujGkRepW69xBN6rzS8MgZoG/view?usp=sharing]. 

The goal-aware bot can deal with 7 goals: "share_personal_problems", 
"get_book_recommendation", "get_series_recommendation", "test_bot",
"get_book_information", "get_travel_recommendation" and "have_fun".

To detect these goals service human_goals_detector (annotators/human_goals_detector) was developed.
This service is a part of annotators module and it is called after receiving user
utterance. It detects goals based on the set of patterns created for each goal.
Detected goals are then stored in the annotations part of the Dialogue State.

To achieve goals, seven dialogue skills were created:

• skills/dff_share_problems_skill

• skills/dff_book_recommendation_skill

• skills/dff_get_book_information_skill

• skills/dff_series_recommendation_skill

• skills/dff_travel_recommendation_skill

• skills/dff_have_fun_skill

• skills/dff_test_bot_skill

Each skill contains from one to five Dialogue Games depending on the formulation of user
request. Every skill node returns a status of goal completion. The user does
not necessarily express their goal explicitly, but at the same time their request
can be close to the topic of some of the goal-related skills. In this case, the bot
offers the user a goal that the user can either accept or reject. Then the skill
returns "goal_offered" status.

To monitor the process of detecting, storing and achieving the goals,
Goal Tracker (annotators/goals_tracker) was developed. Goal Tracker is an annotator that is called
after human_goals_detector. It updates state of user goals for the last bot
response and for the current user utterance and stores it the attributes of the
Dialogue State.

Finally, the Skill Selector (skill_selectors/rule_based_selector) was changed so that it 
chooses skills considering goals state.

## To speak with the bot

### Clone the repo

```
git clone https://github.com/Kpetyxova/goal-aware-dream.git
```

### Chekout to feat/goals branch

```
git checkout feat/goals
```

### Run Goal-Aware Dream distribution

```
docker-compose -f docker-compose.yml -f assistant_dists/dream/docker-compose.override.yml -f assistant_dists/dream/dev.yml -f assistant_dists/dream/proxy.yml  up --build
```

### Let's chat
In a separate terminal tab run:

```
docker-compose exec agent python -m deeppavlov_agent.run -pl assistant_dists/dream/pipeline_conf.json
```

Enter your username and have a chat with Goal-Aware version of Dream!


The README.md for original DREAM can be found [here](https://github.com/Kpetyxova/goal-aware-dream/tree/main#deeppavlov-dream).
