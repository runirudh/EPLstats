# EPLstats - draft 
Multi layer prediction for state change in a soccer match


## Description:

- All soccer matches start at 0-0 goals for each team. 

- Assume Team names to be A & B.

- Starting state for this random phenomenon is (0,0) , from where it can go to state 
  (0,1) or state (1,0) or stay in (0,0) depending on the maximum transition probability 
  (Bayes Decision Rule) out of the 3. 

**Getting these transition probability of changing states is where most of the work 
  needs to be put in.** These probabilities need to be estimated from features that 
  summarize the game situation, team stats (position in table), home/away record,
  how good a team's reaction is after having conceded a goal, etc.
  
- Once we have these transition probabilities, we can fit a big model with mutliple layers
  , where each layer is supplied with the probabilities of state change or state retained, 
  and we simply backpropogate on the most likely path. 
  
- For model architechture a discrete time horizon is applied, which has 6 layers, 
  whose continuous counterpart should be able to tell the state of the game for each minute.


![IMG_0471](https://user-images.githubusercontent.com/96305841/149665581-909c3511-2a01-42ce-b404-3148d16a41e0.jpg)

- Predictions are of the nature- 
  given Team A and B are to play, at team A's home ground
  what is the probability that team A scores first, team B scores first, no one scores.
  This gives us the input for our 2nd layer, basically the state of the game after going 
  through the first layer. We apply more layers till we arrive at the output. 
  Probability that a team scores or does not score is to be estimated by- 
  
  a) team's rank 
  
  b) home/ away record
  
  c) match location
  
  d) goals scored, goals against
  
  e) team wins/loss/draws 
  
  f) **team's response to a conceded goal** // data for this needs to be added, in particular the order of goals leading to final scoreline
    <in particular time horizon is of little interest, since it does not seem likely
     that a team scores in the first half or the second half (atleast for learning). Whereas a hypothesis of 
     a team scoring after having been scored on, or a team's ability to hold onto a lead
     seems to have some merit to it> 
     
     If we have this information we can add rewards to our chain and build a markov decision process problem, 
     & traverse the chain so as to max./min reward.
  
  g) Transfer budget   

Using **data from 2020-21 season** to be able to test our predictions on full range of data.

## all match scores data
[epl-2020-GMTStandardTime.xlsx](https://github.com/runirudh/EPLstats/files/7877241/epl-2020-GMTStandardTime.xlsx) from [link](https://fixturedownload.com/results/epl-2020)

## final league standings data along w/ home & away record for all 9 features
[soccer-standings.xlsx](https://github.com/runirudh/EPLstats/files/7879089/soccer-standings.xlsx) from [link](https://www.rotowire.com/soccer/league-table.php?season=2020)

## data for matches w/ order of score progression
// if this data is found with time of goal attribute, we can try a simple poisson model to see how long before a goal is scored.  
....


## Stages:
1. EDA : printing out the data, checking data types, summary stats.
2. Visual EDA : describe the season stories. Learn about the features, and correlations between match pairings & result.
3. Defining type of regression for first layer, model selection-
4. Fit model for first layer, test to see who scores first goal, or if no one does 
5. Reassess model choice, output type
6. applying same model output flow onto multiple layers, build connected network.    
7. test individual layers manually, feeding output of prev layer as input 
8. test on training data to predict multiple values of goal progression for home & away.
9. assess model capabilities. assign test metrics. 
10. test more on new season data which is halfway completed. train again, predict on remaining games.
    - adding information for utilized transfer budget, how do the changes compare to new standings.
    - is transfer budget a positive addition to teams.
    - add manager change categorical variable.
    - what are factors (based on model coefs) that predict a team's rise/downfall 
