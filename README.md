# EPLstats
Multi layer prediction for state change in a soccer match

#### draft 

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
  and we simply backpropogate on the most likely path on the Markov chain. 
  
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
    <in particular time horizon is of little interest, since it does not seem logical 
     that a team scores in the first half or the second half. Whereas a hypothesis of 
     a team scoring after having been scored on, or a team's ability to hold onto a lead (parking the bus) 
     seems to have some merit to it>
  
  g) Transfer budget   
  
  More predictor variables can be added. But it needs to be ascertained that these aren't correlated and are iid.  
  

LIVE DATA would make for a better model utilizing more features, but here using **data from 
2020-21 season** to be able to test on our predictions on full range of data.

## all match scores data
[epl-2020-GMTStandardTime.xlsx](https://github.com/runirudh/EPLstats/files/7877241/epl-2020-GMTStandardTime.xlsx) from [link](https://fixturedownload.com/results/epl-2020)

## final league standings data along w/ home & away record for all 9 features
[soccer-standings.xlsx](https://github.com/runirudh/EPLstats/files/7879089/soccer-standings.xlsx) from [link](https://www.rotowire.com/soccer/league-table.php?season=2020)

## data for matches w/ order of score progression
....


## Stages:
1. EDA : simply printing out the data, checking data types, getting a feel for it
2. Visual EDA : finding interesting things about teams. possibly leading to better features 
3. Defining type of regression for first layer, model selection
4. Actual fitting of model for 1 layer, test to see who scores first goal, or if no one does 
5. Reassess model choice, output choice
6. Fully connected model.    
7. testing on training data.
8. testing on a team's data for next season which is halfway completed
   - does our model predict man united to do bad in 2020-21 (2nd to 7th)
   - what does Team West Ham's regression coefficient look like in our models (8th to 4th) 
   - adding information for utilized transfer budget, how do the changes compare
