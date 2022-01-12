Here is where you include:
  - Background on your code files:
  I used lab 2 notebook as a template for the project ipynb file. The file contains the code to predict total count of rental bikes rental bikes based on weather and seasonal information using the yellowbrick Bikeshare dataset.
  
  
  - How to run your code, guide to install any additional packages:
  To run my code, just run all cells one by one on the notebook. No need to install any additional packages.
  
  
  - Results, interpretation and reflection:
  Result: ( Please see section 7.2 and 7.3 on notebook.)
  I used LinearRegression, RandomForestRegressor, GradientBoostingRegressor as models and I found RandomForestRegressor performed best among them. Then I tried to find the better model by find the best combination of max_depth and n_estimators. The combination of max_depth = 20 , n_estimators = 100 produced the best validation score.
  
  interpretation: 
  After this project, I became more familiar of using a regression workflow to predict by training models. I used regression models to predict total count of rental bikes rental bikes based on weather and seasonal information using the yellowbrick Bikeshare dataset. I did it by following 8 steps: (Please see the notebook for details)
      1.Load data
      2.Inspect the data
      3.Create trainign and test sets
      4.Compare models using cross-validation
      5.Find a better model
      6.Retrain best model
      7.Evaluate best model on training and test data
  
  reflection:
  I changed my project idea from doing a Kaggle competition of predicting housing prices to current idea. One of the reason is that the data of kaggle competition has 74 features, it is hard to plot all features, correlation heatmap of features with so many features on jupyter notebook. And I also found the competition overall is a bit challenging for me, so I changed my idea.
  The other deviation is that 2.2 Boxplot of features, the units of features are completely different in the dataset compared to same unit of features in lab 2 dataset. So there is no y label in this graph for the project.