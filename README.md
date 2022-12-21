# League of Legends 2022: Secret Winning Tips from Top-Tier Players 

League of Legends (LoL), developed by Riot Games, is the most widely played multiplayer online battle arena (MOBA) video game in the world. In 2020, LoL had more than 100 million monthly active players (https://activeplayer.io/league-of-legends/) and generated revenue of 1.75 billion U.S. dollars in a year (https://www.statista.com/statistics/806975/lol-revenue/). Due to its entertaining and fast-paced gameplay, LoL is one of the most popular eSports in the industry, with an international competitive scene composed of 12 regional leagues. Each year, more than 100 top-tier teams in professional leagues compete against each other in worldwide tournaments to win an enormous prize pool reaching several million dollars (https://www.statista.com/statistics/749024/league-of-legends-championships-prize-pool/). Besides the high prize money, winning the LoL world championship has been considered the highest honor and the ultimate goal for all eSports players. Driven by both incentives, it is crucial for professional teams to identify the determining winning factors and develop appropriate gaming strategies to maximize the probability of victory.
	
  LoL’s gaming mechanics are deliberately designed to have a rigorous evaluation system while preserving unpredictability by inducing complex features across different game stages. In the game, two teams (red or blue) of five players battle in player-versus-player combat to occupy or defend their team’s part of the map. Each player controls a character, known as a “champion”, with unique abilities and different play styles. During the match, the champions collect experience points, upgrade skill levels, earn gold, and purchase items from the store to become more powerful. The goal is to destroy the other team’s base, also called “Neux”. Each base contains a set of resources, including a series of turrets on three lanes, waves of minions that constantly spawn from the inhibitors, monsters within the Jungle, and heralds and drakes. Experience points and gold could be earned from these resources, as well as from killing other champions of the opponent team.  
 
 With the hope of learning from LoL’s top-tier players about their keys to winning, this study aims to identify critical winning factors in professional matches of the game, using the League of Legends eSports match data in 2022. This report consists of three parts. In part one, we tested whether the team’s pre-game factor, being on the red/blue team, is independent of winning the match. In the second part, we looked at the contributing factors to predict the team's total gold, one of the commonly recognized winning factors. In the last part, given the gaming statistics, we developed machine-learning models to identify a winning/losing team. 


### Data source and data dictionary
The data used in the project and the data dictionary explaining all the variables can be found in [here](Data). 

### Code
We implemented our analysis in this [jupyter notebbok](analysis.ipynb). 

### Report
We demonstarted our results and our analysis of the results in this report.

In this report, we used three common data science approaches, inference, prediction, and classification, to answer questions related to the LoL matches.
For the first question about pre-game side selection, by looking at the total winning and losing matches of the red and blue teams, we found that the overall game design was not balanced for the side of the team. In a balanced system, the side of the team should be independent of the game result. However, we could tell from the percentages that blue teams have a higher winning rate than red teams. Taking a closer look at the proportions across different patches, we discovered adjustments made by the developers over time. Since side selections are not always random in tournaments, selecting the advantageous side might be the first step to winning the whole game. Future questions could be asked to investigate the reason underlying such an advantage in side selection by looking at specific champion selections and bans on each side across patches. One should also notice the self-selection bias in this dataset. If the team won from being on the blue side in its previous matches, it is more likely to choose the blue side again in future games. Thus, we could not interpret the dependence as a causal relationship. Time series analysis focusing on the red/blue side selection of specific teams could also be another interesting direction to explore.

For the second question, based on the results of lasso regressions on both dimension-reduced data after PCA and the original standardized data, the length of the game, damage to champions, towers, vision score, different types of kills, and assists are the contributing factors in predicting the total gold of the team. One limitation of our PCA analysis is that the standardization performed before conducting PCA might amplify variables with low columns. In addition, the variable loadings on the components are not distinct enough for us to clearly interpret each component. Even though the components are not correlated, the collinearity between variables still exists when analyzing the loadings of each component, making it hard to perform efficient feature selection based on the loadings.

For the last question, the logistic regression and random forest model results show that assists, deaths, earned gold, and total gold are key winning factors. Our analysis in part three confirmed our expectation in part two that gold is a vital gaming metric impacting the game result. Additionally, even though the number of team kills is a crucial factor in total gold prediction, it does not weigh the same importance in winning the game. In contrast, team total deaths became more important in determining the game result. In other words, it might not matter how many kills a team made throughout the game, but to win the game, one must have fewer deaths. Moreover, by ranking the importance of variables in both models, heralds and barons are not as important as dragons and elders in winning the game, which could be tied back to our first conclusion about the advantage of selecting the blue side. The reason is that dragons and elders are near the blue side of the jungle, whereas heralds and barons are near the red part. One limitation of this analysis is that we used outcome features to classify the outcome. This issue became more prominent in our random forest model since the number of towers and inhibitors are part of the embedded rules in evaluating victory. Thus, they would be and should be important winning factors. More than 2/3 of the variables are information collected after the game ends. If we only use the inter-game variables (e.g., gold at 10 min), the accuracy of the logistic regression model would be 74.86%.

All of our models yield great fits of the test data and high accuracy. One of the main reasons behind this is that this project aimed to capture a relatively simple gaming mechanism using a comprehensive dataset. Unlike models that describe real-life events, our model focused on exploring the mechanism in the game of League of Legends, which composes of fewer uncertainties and has an implicit evaluation system designed by the developers. Given that our dataset covered nearly all gaming metrics, it would not be surprising to have great model performance if all variables were added to the model. Aware of this, the goal of this report was to identify the most important factors rather than to develop a best-fit model.

