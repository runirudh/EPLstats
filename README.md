# EPLstats
Multi layer prediction for state change in a soccer match


## Description:

- All soccer matches start at 0-0 goals for each team. 

- Assume Team names to be A & B.

- Starting state for this random phenomenon is (0,0) , from where it can go to state 
  (0,1) or state (1,0) or stay in (0,0) depending on the maximum probability 
  (Bayes Decision Rule)

**Getting these transition probability of changing states is where most of the work 
  needs to be put in.** These probabilities need to be estimated from features that 
  summarize the game situation, team stats (position in table), home/away record,
  how good a team's reaction is after having conceded a goal, etc.
  
- Once we have these transition probabilities, we can fit a model with mutliple layers
  , where each layer is supplied with the probabilities of state change or state retained.
  
- For model architechture a discrete time horizon is applied, which has 6 layers, 
  whose continuous counterpart should be able to tell the state of the game for each minute.


![IMG_0471](https://user-images.githubusercontent.com/96305841/149665581-909c3511-2a01-42ce-b404-3148d16a41e0.jpg)

LIVE DATA would make for a better model utilizing more features, but here using **data from 
2020-21 season** to be able to test predictions.

[epl-2020-GMTStandardTime.xlsx](https://github.com/runirudh/EPLstats/files/7877241/epl-2020-GMTStandardTime.xlsx) from [link] (https://fixturedownload.com/results/epl-2020)





