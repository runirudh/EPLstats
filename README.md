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
  summarize the game situation, team stats (position in table), home/away record, A v/s B past record,
  how good a team's reaction is after having conceded a goal, etc. 
  The idea is to calculate parameters which after multiplying with feature matrix give out the intended result of the game.
  
- Once we have these transition probabilities, we can fit a big model with mutliple layers
  , where each layer is supplied with the probabilities of state change or state retained, 
  and we simply backpropogate on the most likely path. 
  

![IMG_0471](https://user-images.githubusercontent.com/96305841/149665581-909c3511-2a01-42ce-b404-3148d16a41e0.jpg)
![IMG_0189](https://user-images.githubusercontent.com/96305841/161407453-5568f30e-b074-4cc4-a7e0-97199dbdfbc3.jpg)

- Predictions are of the nature- 
  given Team A and B are to play, at team A's home ground
  what is the probability that team A scores first, team B scores first, no one scores.
  This gives us the input for our 2nd layer, basically the state of the game after going 
  through the first layer. We apply more layers till we reach end of the game. 
 
## initial results from modeling [https://github.com/runirudh/EPLstats/blob/main/epl1.ipynb]

### Decision tree fit for multi-o/p multi-class: 'Home goals' , 'Away Goals' 
    - interpreting each goal as a category
    - pruning tree to find least impurities path
![Screen Shot 2022-04-01 at 9 04 30 PM](https://user-images.githubusercontent.com/96305841/161358242-9bf98d16-c4a5-4b6d-bebf-866c21ceceff.png)

### Decision tree fit for One Hot encoded multi-o/p multi-class: 'Home goals' , 'Away Goals'
    - predicting for each match row, a sparse vector of one hot encoded values for home, away scores (mutually exc. & exh.)

![Screen Shot 2022-04-01 at 9 12 09 PM](https://user-images.githubusercontent.com/96305841/161359538-fb7a6234-73b6-4822-9204-d533632253f6.png)


## data 
https://github.com/tara-nguyen/english-premier-league-datasets-for-10-seasons

Description: EPL data of 10 seasons, with half time & full time score information for each game w/ dates.


![Screen Shot 2022-04-01 at 9 19 36 PM](https://user-images.githubusercontent.com/96305841/161359888-ee970bb1-915f-4e82-9d0c-80422a7ad53b.png)

![Screen Shot 2022-04-01 at 9 22 10 PM](https://user-images.githubusercontent.com/96305841/161360000-e11a058e-a7d0-4503-88c5-59d61de1628e.png)

## all match scores data
[epl-2020-GMTStandardTime.xlsx](https://github.com/runirudh/EPLstats/files/7877241/epl-2020-GMTStandardTime.xlsx) from [link](https://fixturedownload.com/results/epl-2020)

## final league standings data along w/ home & away record for all 9 features
[soccer-standings.xlsx](https://github.com/runirudh/EPLstats/files/7879089/soccer-standings.xlsx) from [link](https://www.rotowire.com/soccer/league-table.php?season=2020)




