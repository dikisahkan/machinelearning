# **README**
Please, read this before before you continue to read / run the Jupyter Notebook file.

This notebook is created as a third capstone project for me to participate in Data Science & Machine Learning course in Purwadhika. The notebook is about doing basic / general steps of machine learning modeling. So this is my portfolio to work on my learning journey towards data science. This modeling might have some flaws, but i tried my best. ;D

The dataset used here is a Bike Sharing data. It's attached in this repo or you can also download it through Kaggle [here](https://www.kaggle.com/competitions/bike-sharing-demand/data) for recent file version.

You can see the presentation version [here](https://www.canva.com/design/DAFosY34nYE/uSyt3Ni0WvF_Y9WGkEgyFg/view?utm_content=DAFosY34nYE&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)

---
## **What did i do in this machine learning modeling?**
Capital Bikeshare is a prominent bike-sharing program operating in the Washington, D.C. metropolitan area.
Dataset from 2011 and 2012.

**Problem**  
Entering new year cycle (2013) and expanding to new locations.

**Goals**  
Capital Bikeshare's Business Strategic team needs a tool that can create predictions of potential customers.

**Analytics Approach**  
Find out relation or impact of X (independent variables) to Y (target being learned and predicted)

**Metric Evaluation**  
- **MAE** - Mean of Absolute Error
- **MAPE** - Mean of Absolute Percentage Error - *(our main metric)*
- **MSE** - Mean of Squared Error
- **RMSE** - Root of Mean Squared Error

### **Step By Step**
#### **1. Data Understanding**
Here, i just learn about the Features compared to the Target. Are they correlates each other? is there any pattern in the Features that can help the model to learn the Target?

Dataset used here is a total customers day-to-day based on environmental variable from 2011 to 2012.

Here's the glossary of each column:  
**datetime** -  hourly date + timestamp  
**humidity** -  relative humidity  
**weathersit** -1: Clear, Few clouds, Partly cloudy, Partly cloudy  
                2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist  
                3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds  
                4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog  
**holiday** -   whether the day is considered a holiday  
**season** -    1 = spring,  
                2 = summer,  
                3 = fall,  
                4 = winter  
**atemp** -     "feels like" temperature in Celsius  
**temp** -      temperature in Celsius  
**hr** -        time of rent (hour)  
**casual** -    number of non-registered user rentals initiated  
**registered** - number of registered user rentals initiated  
**count** -     number of total rentals

#### **2. Train Test Split**
The features are: month, hum, weathersit, holiday, season, temp, hr, dayDate, dayName, year, weekdays.  
The targets are: Casual, Registered, and Cnt.  
Casual + Registered = Cnt.  
So, our main target is Cnt.

#### **3. Model Benchmarking**
This is the list of initial models  
```
from sklearn.linear_model import LinearRegression
from sklearn.neighbors import KNeighborsRegressor
from sklearn.tree import DecisionTreeRegressor
from sklearn.svm import SVR
from sklearn.ensemble import RandomForestRegressor
from xgboost import XGBRegressor
from sklearn.linear_model import Ridge
from sklearn.linear_model import Lasso
from sklearn.ensemble import GradientBoostingRegressor  
```

We got `XGBoostRegressor` and `RandomForestRegressor` with top two best score to hypertune.

#### **4. Model Hypertune**
Model terbaik adalah **Tuned** `XGBoostRegressor`.
```
{'model__regressor__learning_rate': 0.11,
 'model__regressor__max_depth': 6,
 'model__regressor__n_estimators': 300}
 ```

#### **5. Fit to Test**
**Train Accuracy**: 0.978136  
**MAE**: 23.067434  
**MAPE**: 0.223276  
**MSE**: 1451.567146
**RMSE**: 38.099438

### **Conclusion**
- Selected Models: `XGBRegressor()` (MAPE ~24.5%, MAE ~25.6) and `RandomForestRegressor()` (MAPE ~27.7%, MAE ~28).
- Best Model: Tuned `XGBRegressor()` (MAPE ~23.5%, MAE ~24).
- Test Set Performance: Improved to MAPE ~22% and MAE ~23, indicating accurate predictions for new data.
- Model Range: Best performance within 1-970 total customers, potentially less accurate outside this range.
- MAPE Interpretation: 22% error in predicting total customers, justified by MAE (~23), indicating better accuracy for higher numbers.
- Feature Importance: Key predictors are hour, weekdays, year, seasons, and temperature.
- Business Insights: Facilitates forecasting future customers and suggests growth in the coming year.
- Location Expansion: Predictions rely on temperature, humidity, and weather rather than specific location features.

### **Recommendation**
- Analyze confusing patterns in features to improve accuracy for low number predictions.
- Incorporate additional environmental variables to refine location-specific predictions during business expansion.
- Leverage the tuned `XGBRegressor()` model to effectively predict total customers within the range of 1 to 970. 
- Explore advanced modeling techniques, such as ensemble models or Recursive Neural Networks (RNN)
- Uncover additional insights by investigating alternative targets, such as "Registered" or "Casual" riders, or exploring combined approaches.

---
###### **This notebook is created by Diki Renanda / @dikisahkan. You can reach me through any social media GitHub, Kaggle, Medium, LinkedIn, IG, and TikTok.**