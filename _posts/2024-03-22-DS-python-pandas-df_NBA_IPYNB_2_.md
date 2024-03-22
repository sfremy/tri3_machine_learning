---
layout: post
toc: True
title: ML, NBA Data
description: None
courses: {'csp': {'week': 25}}
type: ccc
---

```python
# Uncomment the following lines to install the required packages
!pip install opendatasets #download the data set
!pip install pandas #data manipulation and analysis
```

    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: opendatasets in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (0.1.22)
    Requirement already satisfied: tqdm in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from opendatasets) (4.66.2)
    Requirement already satisfied: kaggle in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from opendatasets) (1.6.6)
    Requirement already satisfied: click in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from opendatasets) (8.1.7)
    Requirement already satisfied: six>=1.10 in /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/site-packages (from kaggle->opendatasets) (1.15.0)
    Requirement already satisfied: certifi in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from kaggle->opendatasets) (2023.7.22)
    Requirement already satisfied: python-dateutil in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from kaggle->opendatasets) (2.8.2)
    Requirement already satisfied: requests in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from kaggle->opendatasets) (2.31.0)
    Requirement already satisfied: python-slugify in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from kaggle->opendatasets) (8.0.4)
    Requirement already satisfied: urllib3 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from kaggle->opendatasets) (2.0.7)
    Requirement already satisfied: bleach in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from kaggle->opendatasets) (6.1.0)
    Requirement already satisfied: webencodings in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from bleach->kaggle->opendatasets) (0.5.1)
    Requirement already satisfied: text-unidecode>=1.3 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from python-slugify->kaggle->opendatasets) (1.3)
    Requirement already satisfied: charset-normalizer<4,>=2 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from requests->kaggle->opendatasets) (3.3.1)
    Requirement already satisfied: idna<4,>=2.5 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from requests->kaggle->opendatasets) (3.4)
    
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m A new release of pip is available: [0m[31;49m23.3.2[0m[39;49m -> [0m[32;49m24.0[0m
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m To update, run: [0m[32;49m/Library/Developer/CommandLineTools/usr/bin/python3 -m pip install --upgrade pip[0m
    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: pandas in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (2.2.1)
    Requirement already satisfied: numpy<2,>=1.22.4 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from pandas) (1.26.4)
    Requirement already satisfied: python-dateutil>=2.8.2 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from pandas) (2.8.2)
    Requirement already satisfied: pytz>=2020.1 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from pandas) (2023.4)
    Requirement already satisfied: tzdata>=2022.7 in /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages (from pandas) (2024.1)
    Requirement already satisfied: six>=1.5 in /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/site-packages (from python-dateutil>=2.8.2->pandas) (1.15.0)
    
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m A new release of pip is available: [0m[31;49m23.3.2[0m[39;49m -> [0m[32;49m24.0[0m
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m To update, run: [0m[32;49m/Library/Developer/CommandLineTools/usr/bin/python3 -m pip install --upgrade pip[0m



```python
import opendatasets as od
import pandas

od.download('https://www.kaggle.com/datasets/vivovinco/20222023-nba-player-stats-regular')

```

    Please provide your Kaggle credentials to download this dataset. Learn more: http://bit.ly/kaggle-creds
    Your Kaggle username:Your Kaggle Key:

    /Users/rayanesouissi/Library/Python/3.9/lib/python/site-packages/urllib3/__init__.py:34: NotOpenSSLWarning: urllib3 v2.0 only supports OpenSSL 1.1.1+, currently the 'ssl' module is compiled with 'LibreSSL 2.8.3'. See: https://github.com/urllib3/urllib3/issues/3020
      warnings.warn(


    Downloading 20222023-nba-player-stats-regular.zip to ./20222023-nba-player-stats-regular


    100%|██████████| 43.4k/43.4k [00:00<00:00, 2.58MB/s]

    


    



```python
import pandas as pd

df = pd.read_csv('20222023-nba-player-stats-regular/2022-2023 NBA Player Stats - Playoffs.csv', encoding='cp1252', sep=';')

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rk</th>
      <th>Player</th>
      <th>Pos</th>
      <th>Age</th>
      <th>Tm</th>
      <th>G</th>
      <th>GS</th>
      <th>MP</th>
      <th>FG</th>
      <th>FGA</th>
      <th>...</th>
      <th>FT%</th>
      <th>ORB</th>
      <th>DRB</th>
      <th>TRB</th>
      <th>AST</th>
      <th>STL</th>
      <th>BLK</th>
      <th>TOV</th>
      <th>PF</th>
      <th>PTS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bam Adebayo</td>
      <td>C</td>
      <td>25</td>
      <td>MIA</td>
      <td>23</td>
      <td>23</td>
      <td>37.0</td>
      <td>7.3</td>
      <td>15.1</td>
      <td>...</td>
      <td>0.821</td>
      <td>2.7</td>
      <td>7.1</td>
      <td>9.9</td>
      <td>3.7</td>
      <td>0.9</td>
      <td>0.7</td>
      <td>2.7</td>
      <td>3.1</td>
      <td>17.9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Santi Aldama</td>
      <td>PF</td>
      <td>22</td>
      <td>MEM</td>
      <td>6</td>
      <td>0</td>
      <td>16.8</td>
      <td>2.5</td>
      <td>5.5</td>
      <td>...</td>
      <td>1.000</td>
      <td>1.2</td>
      <td>3.2</td>
      <td>4.3</td>
      <td>1.2</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.3</td>
      <td>0.8</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Nickeil Alexander-Walker</td>
      <td>SG</td>
      <td>24</td>
      <td>MIN</td>
      <td>5</td>
      <td>4</td>
      <td>29.6</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>...</td>
      <td>0.667</td>
      <td>0.2</td>
      <td>1.8</td>
      <td>2.0</td>
      <td>1.4</td>
      <td>0.6</td>
      <td>0.2</td>
      <td>0.8</td>
      <td>1.8</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Grayson Allen</td>
      <td>SG</td>
      <td>27</td>
      <td>MIL</td>
      <td>5</td>
      <td>5</td>
      <td>29.8</td>
      <td>3.8</td>
      <td>8.2</td>
      <td>...</td>
      <td>0.857</td>
      <td>0.2</td>
      <td>2.2</td>
      <td>2.4</td>
      <td>1.8</td>
      <td>0.4</td>
      <td>0.0</td>
      <td>0.8</td>
      <td>1.4</td>
      <td>11.6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Jarrett Allen</td>
      <td>C</td>
      <td>24</td>
      <td>CLE</td>
      <td>5</td>
      <td>5</td>
      <td>38.2</td>
      <td>4.4</td>
      <td>7.2</td>
      <td>...</td>
      <td>0.500</td>
      <td>3.0</td>
      <td>4.4</td>
      <td>7.4</td>
      <td>2.4</td>
      <td>0.8</td>
      <td>1.0</td>
      <td>0.6</td>
      <td>2.0</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>212</th>
      <td>213</td>
      <td>Ziaire Williams</td>
      <td>SF</td>
      <td>21</td>
      <td>MEM</td>
      <td>4</td>
      <td>0</td>
      <td>3.0</td>
      <td>0.5</td>
      <td>1.8</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.3</td>
      <td>1.3</td>
    </tr>
    <tr>
      <th>213</th>
      <td>214</td>
      <td>Trae Young</td>
      <td>PG</td>
      <td>24</td>
      <td>ATL</td>
      <td>6</td>
      <td>6</td>
      <td>38.3</td>
      <td>10.0</td>
      <td>24.8</td>
      <td>...</td>
      <td>0.860</td>
      <td>0.8</td>
      <td>2.8</td>
      <td>3.7</td>
      <td>10.2</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>4.0</td>
      <td>1.8</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>214</th>
      <td>215</td>
      <td>Omer Yurtseven</td>
      <td>C</td>
      <td>24</td>
      <td>MIA</td>
      <td>8</td>
      <td>0</td>
      <td>2.0</td>
      <td>0.3</td>
      <td>0.9</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.4</td>
      <td>0.3</td>
      <td>0.6</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.1</td>
      <td>0.3</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>215</th>
      <td>216</td>
      <td>Cody Zeller</td>
      <td>C</td>
      <td>30</td>
      <td>MIA</td>
      <td>21</td>
      <td>0</td>
      <td>8.3</td>
      <td>1.0</td>
      <td>1.7</td>
      <td>...</td>
      <td>0.400</td>
      <td>0.5</td>
      <td>1.8</td>
      <td>2.3</td>
      <td>0.3</td>
      <td>0.1</td>
      <td>0.2</td>
      <td>0.6</td>
      <td>1.3</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>216</th>
      <td>217</td>
      <td>Ivica Zubac</td>
      <td>C</td>
      <td>25</td>
      <td>LAC</td>
      <td>5</td>
      <td>5</td>
      <td>26.0</td>
      <td>3.4</td>
      <td>6.0</td>
      <td>...</td>
      <td>0.750</td>
      <td>3.2</td>
      <td>6.4</td>
      <td>9.6</td>
      <td>0.6</td>
      <td>0.6</td>
      <td>0.2</td>
      <td>2.2</td>
      <td>1.6</td>
      <td>9.2</td>
    </tr>
  </tbody>
</table>
<p>217 rows × 30 columns</p>
</div>



#### Median PPG Among NBA Players


```python
df['PTS'].median()
```




    6.5



#### Range (Maximum - Minimum Values) of NBA Players


```python
df['PTS'].max() - df['PTS'].min()
```




    34.5



#### Average Field Goals Made Among Players


```python
df['FG'].mean()
```




    3.193548387096774




```python
#Clean data
df_new = df[['Age', 'FG', 'FG%', '3P', '3P%', 'FT', 'FT%']] 

df_new
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>FG</th>
      <th>FG%</th>
      <th>3P</th>
      <th>3P%</th>
      <th>FT</th>
      <th>FT%</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>25</td>
      <td>7.3</td>
      <td>0.481</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>3.4</td>
      <td>0.821</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22</td>
      <td>2.5</td>
      <td>0.455</td>
      <td>1.2</td>
      <td>0.467</td>
      <td>0.3</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>24</td>
      <td>3.0</td>
      <td>0.429</td>
      <td>2.0</td>
      <td>0.400</td>
      <td>0.4</td>
      <td>0.667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>27</td>
      <td>3.8</td>
      <td>0.463</td>
      <td>2.8</td>
      <td>0.483</td>
      <td>1.2</td>
      <td>0.857</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24</td>
      <td>4.4</td>
      <td>0.611</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.6</td>
      <td>0.500</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>212</th>
      <td>21</td>
      <td>0.5</td>
      <td>0.286</td>
      <td>0.3</td>
      <td>0.333</td>
      <td>0.0</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>213</th>
      <td>24</td>
      <td>10.0</td>
      <td>0.403</td>
      <td>3.0</td>
      <td>0.333</td>
      <td>6.2</td>
      <td>0.860</td>
    </tr>
    <tr>
      <th>214</th>
      <td>24</td>
      <td>0.3</td>
      <td>0.286</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>215</th>
      <td>30</td>
      <td>1.0</td>
      <td>0.571</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.3</td>
      <td>0.400</td>
    </tr>
    <tr>
      <th>216</th>
      <td>25</td>
      <td>3.4</td>
      <td>0.567</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>2.4</td>
      <td>0.750</td>
    </tr>
  </tbody>
</table>
<p>217 rows × 7 columns</p>
</div>




```python
# Import the train_test_split function for splitting data into train and test sets
from sklearn.model_selection import train_test_split
# Import the DecisionTreeClassifier for decision tree modeling
from sklearn.tree import DecisionTreeClassifier
# Import the LogisticRegression for logistic regression modeling
from sklearn.linear_model import LogisticRegression
# Import the accuracy_score function to compute the accuracy of predictions
from sklearn.metrics import accuracy_score

# Define a function to replace scores greater than 10 with 1, otherwise 0
def replace_score(score):
    if score > 10:
        return 1
    else:
        return 0

# Prepare the feature matrix (x) and target vector (y) based on the 'PTS' column
x = df_new  # Assumes df_new is a pre-processed DataFrame ready for modeling
y = df['PTS'].apply(replace_score)  # Apply the replace_score function to each point value

# Split the dataset into training and testing sets, with 30% of data as test set, and a fixed random state for reproducibility
X_train, X_test, y_train, y_test = train_test_split(x, y, test_size=0.3, random_state=42)

# Initialize and train a decision tree classifier on the training data
dt = DecisionTreeClassifier()
dt.fit(X_train, y_train)

# Make predictions on the test set and calculate the accuracy of the decision tree model
y_pred = dt.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print('DecisionTreeClassifier Accuracy: {:.2%}'.format(accuracy))  # Print the accuracy of the decision tree model

# Initialize and train a logistic regression model on the training data
logreg = LogisticRegression()
logreg.fit(X_train, y_train)

# Make predictions on the test set and calculate the accuracy of the logistic regression model
y_pred = logreg.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print('LogisticRegression Accuracy: {:.2%}'.format(accuracy))  # Print the accuracy of the logistic regression model
```

    DecisionTreeClassifier Accuracy: 93.94%
    LogisticRegression Accuracy: 98.48%



```python
from sklearn import svm
from sklearn import datasets

from joblib import dump, load

dump(logreg, 'nba_model_save.joblib') 
```




    ['nba_model_save.joblib']



### Predicting Survival
So, now we are ready to play the game... "Would I have survived the Titanic?".  

Insert your own data in the code.  Look at your analysis and consider how you would travel today.
- Data description:
    - pclass - Passenger Class (1 = 1st; 2 = 2nd; 3 = 3rd)
    - name - Name
    - sex - male or female
    - age - number of year 
    - sibsp - number of Siblings/Spouses Aboard
    - parch - number of Parents/Children Aboard
    - fare - passenger fare 0 to 512
    - embarked - Port of Embarkation (C = Cherbourg; Q = Queenstown; S = Southampton)
    - alone - boolean True or False


```python
import numpy as np  # Importing the NumPy library for numerical operations

# Define a new player's data as a DataFrame with specific basketball-related statistics
player = pd.DataFrame({
    'Age': [29],  
    'FG': [10],    
    'FG%': [.2],  
    '3P': [4],    
    '3P%': [.20],  
    'FT': [2],    
    'FT%': [1],   
})

# Use the trained logistic regression model (logreg) to predict the probability
# of scoring less than 10 points ('dead') and more than 10 points ('alive')
above10_proba, below10_proba = np.squeeze(logreg.predict_proba(player))

# Print the predicted probabilities for scoring less than 10 and more than 10 points
print('below 10 PPG probability: {:.2%}'.format(below10_proba))  
print('above 10 PPG probability: {:.2%}'.format(above10_proba))
```

    below 10 PPG probability: 100.00%
    above 10 PPG probability: 0.00%

