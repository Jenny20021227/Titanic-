# Titanic🛳 
This project is a comprehensive analysis and predictive modeling challenge based on the Titanic dataset, implemented entirely in R. The goal was to explore the dataset through visualization, identify key features related to passenger survival, and build a machine learning model to predict survival outcomes for unseen test data.

📁 Dataset Overview

Three CSV files were used:

train.csv: Passenger data including survival information (used for training)
test.csv: Passenger data without survival labels (used for prediction)
sample_submission.csv: Format for the prediction output
Key variables included:

Pclass: Ticket class (1st, 2nd, 3rd)
Sex, Age
SibSp, Parch: Number of siblings/spouses or parents/children aboard
Fare, Cabin, Embarked: Fare paid, cabin info, port of embarkation

📊 Exploratory Data Analysis (EDA)

Using ggplot2, we visualized survival patterns across key variables:

▶️ Survival Rate by Sex
Female passengers had significantly higher survival rates than males.
<img width="691" alt="survival_by_sex" src="https://github.com/user-attachments/assets/2d2df034-69ce-458b-b98f-efd31b59d894" />

▶️ Survival Rate by Passenger Class
1st class passengers were far more likely to survive than those in 3rd class.
<img width="691" alt="survival_by_class" src="https://github.com/user-attachments/assets/7de728e9-537f-4952-b439-41bcbcc665b7" />

▶️ Age and Fare Distributions
Younger children (especially under 10) had higher survival rates.
Passengers who paid higher fares generally had better outcomes, especially in 1st class.
<img width="691" alt="age_distribution" src="https://github.com/user-attachments/assets/33560d65-d161-4374-8200-683dfdd7402f" />

▶️ Survival Rate by Family Size & Alone Status
We engineered:

FamilySize = SibSp + Parch + 1
IsAlone = TRUE if FamilySize == 1
We discovered:

Solo travelers had lower survival rates.
Small families (2–4 members) had better survival rates.
<img width="691" alt="survival_by_family_size" src="https://github.com/user-attachments/assets/79008296-5e00-47ee-bf7e-038add2d4e7f" />
<img width="691" alt="survival_by_isalone" src="https://github.com/user-attachments/assets/88b85700-62f5-4ef3-aceb-a7e8eb1c315b" />

▶️ Top 5 and Bottom 5 Survival Rate Groups
By grouping passengers by combinations of Sex, Pclass, and FamilySize, we identified:

Top 5 Groups (e.g., female_1_2) with survival rates near 100%
Bottom 5 Groups (e.g., male_3_1) with survival rates near 0%
This highlighted the real-world impact of social status, gender, and family.
<img width="691" alt="top_bottom_groups" src="https://github.com/user-attachments/assets/5ab4762c-2493-4282-ad0d-6dd854f6206a" />

🤖 Modeling with Random Forest

We trained a Random Forest model using the following features:
Survived ~ Pclass + Sex + Age + Fare + Embarked + FamilySize + IsAlone 

Categorical variables were properly encoded as factor().
Missing Age and Fare values were imputed using median values.
The model was trained on train.csv and used to predict Survived on test.csv.

📈 Final Predictions

The predictions for test.csv were saved to:
submission.csv
The file includes the predicted survival (0 = died, 1 = survived) for each passenger in the test set, ready for Kaggle submission.

✅ Survived: Passenger 896
PassengerId: 896
Prediction: Survived = 1
Likely features:
Sex: Female
Pclass: 1st class
Fare: High
FamilySize: 2 (not alone)
Age: ~30
Explanation:
Passenger 896 likely survived because she had a combination of high-survival features:

She was a female, which the data shows had a much higher chance of survival.
She was in 1st class, which also had the highest survival rate.
She had family members aboard, which the model may associate with higher survival (especially for women).
Her fare and cabin access may also reflect higher social status, further boosting survival probability.

✅ Survived: Passenger 898
PassengerId: 898
Prediction: Survived = 1
Explanation:
Although we don’t have exact feature values listed here, the model likely found similar patterns — female, better class, not alone — which are known high-survival signals.

❌ Did Not Survive: Passenger 892
PassengerId: 892
Prediction: Survived = 0
Likely features:
Sex: Male
Pclass: 3rd class
Fare: Low
FamilySize: 1 (alone)
Cabin: Missing
Explanation:
Passenger 892 likely had low-survival features:

He was male and in 3rd class, which combined result in low survival rates.
He likely had no family with him.
Lower fare and no cabin information may reflect a lower social standing.
The model, based on its training, likely associated this profile with poor chances of survival.

❌ Did Not Survive: Passenger 894
PassengerId: 894
Prediction: Survived = 0
Explanation:
This passenger likely matched the pattern of male + 3rd class + alone, or lacked other protective features like a high fare or family. Based on similar passengers in the training data, the model assigned a low probability of survival.

🎯 Summary

The model made decisions based on patterns it observed in the training data:

Feature	         /        Higher Survival / Lower Survival

Sex	             /             Female	    /      Male

Class(Pclass)	   /             1st class	 /   3rd class

Age              /   	Young children (<10) /	Middle-aged males

Family	              Small families (2–4) /	Alone or very large group

Fare	            /            High fare	   /     Low fare

Title	            /         Miss,Mrs,Master	 /   Mr, Other

These rules were learned through data, not manually coded.

🧠 What I Learned

Through this project, I gained hands-on experience in:

Real-world data cleaning and feature engineering in R

Visual storytelling with ggplot2

Handling missing values, categorical encoding, and data imbalance

Building interpretable machine learning models with randomForest

Producing end-to-end analysis reports using R Markdown to HTML

🕰 Historical and Social Insights

While this project focused on data science and prediction, the Titanic dataset also offered a striking glimpse into the social structure and inequalities of the early 20th century.

Here are some of the most compelling patterns we observed during analysis:

🕰 Historical and Social Insights

While this project focused on data science and prediction, the Titanic dataset also offered a striking glimpse into the social structure and inequalities of the early 20th century.

Here are some of the most compelling patterns we observed during analysis:

🧑‍🤝‍🧑 Family Matters
Passengers who traveled with family (FamilySize 2–4) had better survival rates than those who were alone.
The presence of family may have improved communication and support during evacuation, and perhaps family groups were prioritized together.


🏰 Class Disparity
The survival rate for 1st class passengers was dramatically higher than that of 3rd class passengers.
Wealth and social status clearly played a role in access to lifeboats and evacuation order.
Many 3rd class passengers were located in lower decks, making it physically harder to reach lifeboats quickly.


🎩 Social Titles Reflecting Status
Features like "Title" (Mr, Miss, Mrs, Master, etc.) helped capture nuanced social roles.
Rare titles like "Dr", "Rev", or "Sir" were grouped under “Other” but still reflect the formal social hierarchy of the era.
The fact that the title Master (young boys) showed relatively high survival is also consistent with the focus on saving children.


🚢 Port of Embarkation
Most passengers boarded at Southampton ("S"), but those from Cherbourg ("C") had higher survival rates.
This is likely because many wealthier passengers boarded from Cherbourg, reinforcing how socio-economic status impacted survival.

💬 Conclusion
Through this data, we weren't just predicting outcomes — we were uncovering real human stories shaped by class, gender, age, and access.
The Titanic dataset serves as both a machine learning playground and a powerful reflection of social dynamics from a century ago.
