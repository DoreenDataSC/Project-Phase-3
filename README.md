# Project-Phase-3
# Predicting Customer Churn: Empowering Syriatel to Optimize Retention and Loyalty Utilizing Data-Driven Insights
Syriatel is Syria's leading telecom provider since 2000, offering mobile services and maintaining a strong network despite ongoing challenges.
With a focus on providing the best mobile communications experience, Syriatel aims to empower its customers, enhance employee satisfaction, and achieve sustained value creation for its shareholders. 
# Objectives
outlines the importance of churn prediction insights for SyriaTel, emphasizing the need to identify customer groups at high risk of churning and to understand the contributing factors for developing effective retention strategies. It suggests evaluating various predictive models using metrics like accuracy and F1-score to find the most reliable one. Finally, it recommends targeted marketing, exclusive offers, and improved customer support as strategies to minimize churn and suggests a plan for ongoing churn prediction to enhance customer loyalty.
# Metric For Success
The model's success will be measured by its churn prediction accuracy and its effects on customer retention, revenue, and satisfaction
- **Accuracy**: Correct churn predictions percentage.
- **Precision**: Predicted churners who actually churn.
- **Recall**: Actual churners identified.
- **F1 Score**: Balance of precision and recall.
- **AUC-ROC**: Distinction between churners and non-churners.
# Data Understanding
The analysis uses data from Kaggle.com to predict churn among Syriatel customers. It includes 3333 rows and 21 columns, detailing customer information like state, account length, subscriptions, and call statistics. Understanding this data is key for preparation and prediction. I moved on to data preparation after the review.
# Data Preperation & Analysis
To prepare the dataset for modeling,:
1. Renamed columns for clarity.
2. Verified there were no missing values or duplicates.
3. Removed irrelevant columns like 'phone number' and 'area code.'
4. Added new features for total charges, calls, and minutes.
5. Converted 'international plan' and 'voice mail plan' into numerical values.
6. Created a new dataset with OneHotEncoding for categorical variables.
7. Dropped unnecessary columns after aggregation.

The final dataset now has 3,333 rows and 12 columns, ready for analysis and customer churn predictions.
# Exploratory Data Analysis
This analysis examines the relationship between customer churn and variables like account length, international plan, voice mail plan, and customer service calls.

**Step 1: Data Visualization**  
I created plots to visualize the impact of these variables on churn:

- **Account Length vs. Churn:** Box plot shows account lengths for churned and non-churned customers.
- **International Plan vs. Churn:** Count plot of churn rates with or without an international plan.
- **Voice Mail Plan vs. Churn:** Similar to the international plan plot.
- **Voice Mail Messages vs. Churn:** Box plot comparing voice mail messages.
- **Customer Service Calls vs. Churn:** Displays call distributions for both groups.
- **Area Code vs. Churn:** Churn rates across different area codes.
- **Monthly Charge vs. Churn:** Compares monthly charges for both groups.
# Step 2: Additional Analysis  
I also examined Total Charges, Total Calls, and Total Minutes through box plots.

# Step 3: Outlier Analysis 
In 'final2_data_df', I identified outliers but chose not to remove them due to their significant proportion (over 30%). Removing them would reduce the dataset substantially (from 3,333 to 653 rows), risking the loss of important information and potentially impacting model performance and generalization.
analyzed the skewness of numerical columns in the dataset:

**Nearly Symmetric Variables:**  
Account Length and Monthly Charge have skewness values near 0 and don’t need transformations.

**Right-Skewed Variables:**  
Number of Voice Mail Messages and Customer Service Calls show moderate to high skewness. Consider log transformations for algorithms sensitive to skewness, while decision trees and random forests may not require them.

**Step 4:**  
I created histograms to visualize distributions and identify skewness.

**Step 5:**  
A heatmap revealed high correlations between total charge and minutes charge, as well as between the voice mail plan (yes) and number of voice mail messages.
# Modelling
**Stage Overview:**

In this stage, we will:

1. Check for multicollinearity using the Variance Inflation Factor (VIF).
2. Apply log transformations where necessary.
3. Standardize features for modeling.
4. Address class imbalance using SMOTE.
5. Implement Logistic Regression and Random Forest models.

**Step 1: Checking for Multicollinearity**

We checked for multicollinearity using VIF:

- **Constant (VIF = 140.14):** High but expected for the intercept.
- **Account Length, Number of Voice Mail Messages, Customer Service Calls, Total Calls (VIF = 1.00):** No correlation with other variables.
- **Monthly Charge (VIF = 194.27) & Total Charges (VIF = 198.86):** Both highly correlated; consider removing one to reduce redundancy.
- **Total Minutes (VIF = 4.88):** Moderate correlation; may be acceptable.

**Key Takeaway:** Keep low VIF variables for the model and consider removing or combining high VIF variables.

**Step 2: Log Transformation**

Post-log transformation, our columns include 'account length', 'number of voice mail messages', and 'churn'. The variable 'number of voice mail messages' showed the least impact from the transformation. We will drop either monthly charges or total charges due to high correlation.

**Step 3: Modeling**

We performed Logistic Regression and Random Forest modeling to predict customer churn after balancing the dataset with SMOTE and standardizing the features. Both models were evaluated to identify the most important predictors of churn.

**Step 4: Data Preparation and Evaluation**

Data was split into training and testing sets, balanced with SMOTE, and standardized. The model's performance was assessed using accuracy, ROC AUC, and confusion matrices.

**Performance Insights:**

The model excels at identifying non-churn customers but struggles with churn predictions. While the overall accuracy is 65.7%, there is room for improvement in identifying customers likely to churn.

**In Conclusion:**

The accuracy is decent, but further consideration of precision, recall, and F1-score is necessary for a comprehensive evaluation.

**Conclusion**  
The Random Forest model outperformed Logistic Regression in predicting customer churn, achieving an accuracy of 87.3% compared to Logistic Regression's 65.7%. It also had higher Precision, Recall, and F1 scores, with a ROC AUC of 0.799 versus 0.736 for Logistic Regression. The number of customer service calls was the most significant feature for predicting churn, accounting for 42% importance, followed by total minutes at 31%. Random Forest demonstrated a better ability to generalize, with a mean cross-validation score of 97.06%, while Logistic Regression scored only 68.32%.

**Recommendation**  
Random Forest is the most effective model for predicting churn. We should focus on reducing customer service calls and increasing total minutes used to lower churn rates. While SMOTE balanced the data, adjusting class weights or exploring different models could enhance predictions. Logistic Regression, despite being less accurate, offers simplicity for quick insights.

**Next Steps**  
- **Test Other Algorithms:** Evaluate different models like Gradient Boosting to find potential improvements over Random Forest.  
- **Create New Features:** Develop or combine features to better capture customer relationships, including demographic data like age.  
- **Improve Model Settings:** Use hyperparameter tuning to optimize model performance, especially for Random Forest.  
- **Implement the Best Model:** Once identified, integrate the best-performing model into business operations for automatic churn prediction.  
- **Continuously Enhance the Model:** Regularly retrain the model with new data to adapt to evolving customer behaviors.
