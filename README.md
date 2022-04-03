# EPLstats - draft 
Multi layer prediction for state change in a soccer match


## Description:

- All soccer matches start at 0-0 goals for each team. 

- Assume Team names to be A & B.

- Starting state for this random phenomenon is (0,0) , from where it can go to state 
  (0,1) or state (1,0) or stay in (0,0) depending on the maximum transition probability 
  (Bayes Decision Rule) out of the 3. 
  
  ![IMG_0189](https://user-images.githubusercontent.com/96305841/161407555-29eb74ca-e9ec-431b-9868-b0aa54f0c371.jpg)

- Assume stationary probabilities {limiting probability of a Markov chain}, based on the fact that given random present state of game 

        X_j = (p,q) , the next state depends only on the present state(which in turn depend on past states)
        
        X_j+1 = (f(p), f(q))
        
        where f is our predicted function of describing probability of going from state 
        
        eg. 3 - 0 given n features {X_1, X_2, X_3...X_n) into only 3 possible states 3-1,3-0,4-0 
        
        We can apply both descriminative (partitioning algos Kneighbors, CART, Decision Trees) & generative models (NB, logistic regression)
        
        to predict these classes(homegoal1, awaygoal1, no change).
        
![IMG_4D5D68F338AB-1](https://user-images.githubusercontent.com/96305841/161445203-d0eec127-caf4-442f-b200-c17894b603b3.jpeg)
     

      
**Getting transition probabilities**
  These probabilities are to be estimated from features that 
  summarize the game situation, team stats (position in table), home/away record, A v/s B past record etc. .
  It may be suitable to do some initial blackbox modeling first before a network is made.
  
- transition probabilities are simply state change(+-) or state retained. 
  
![IMG_0197](https://user-images.githubusercontent.com/96305841/161445667-6281cd62-1a67-4504-b79c-994f7535968a.jpg)

![IMG_0196](https://user-images.githubusercontent.com/96305841/161445259-94458818-7802-4cb7-9656-d443d8ec7e5f.jpg)


- After making prediction on events of A,B scores we update some features of the game & refit the model for the 2nd half.
 
## initial results from modeling final score of game [https://github.com/runirudh/EPLstats/blob/main/epl1.ipynb] 

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




