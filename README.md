# Prediction-Product-Sale 
Author: Hiba Shanti

This project analyzes food sales across various retail outlets to identify the specific products and store locations that drive growth.
This project provides retailers with data-driven insights to help them focus on their most profitable assets

- Original dataset:https://drive.google.com/file/d/1wn6N4Fa6ptsJAeL5wuKL3mmYdAiEqEJE/view?usp=drive_link

- Here is the dictionary for the dataset:

   <img width="744" height="686" alt="Screen Shot 2026-01-08 at 10 08 50 PM" src="https://github.com/user-attachments/assets/49bedf01-4824-4338-8ed1-9459da22f529" />
  



- Summary: I performed a comprehensive Exploratory Data Analysis (EDA), starting with data cleaning to remove duplicates, handle missing values, and resolve inconsistencies. Once the data was refined, I utilized data visualization techniques to examine feature relationships and uncover key patterns, ensuring a high-quality dataset for production.

- Examples of visualized relationships:
 * 1- Correlation Heatmaps: To identify which features drive the most value.
   - Shown the relationship between numerical values in addition to their direction and strength.
<img width="686" height="589" alt="Heatmap" src="https://github.com/user-attachments/assets/193a10d6-9b6b-40b3-b2ee-a8f75e29d0d2" />

* 2- Using csatterplot to display one of the relations in the heatmap :
  - Item maximum retail price (MRP) has a moderate positive relationship with Item_Outlet_Sales
   <img width="589" height="432" alt="Scatterplot" src="https://github.com/user-attachments/assets/ce069d94-9d7c-478c-b12c-cced94041adb" />

* 3- A Boxplot displaying the relationship between Outlet_Location_Type and Item_Outlet_Sales
  - The boxplot reveals a similar median range across all three locations, along with some outliers
 <img width="589" height="433" alt="boxplot" src="https://github.com/user-attachments/assets/7574ec4c-a9c3-46a0-84c4-a3955d37ef47" />





- Modeling Step
  - During the modeling phase, the dataset was separated into ordinal, categorical, and numerical features. Missing values were imputed, categorical features were encoded, and numerical features were scaled when appropriate. Separate preprocessing pipelines were created for each feature type and combined using a ColumnTransformer to ensure consistent and reproducible data preparation.
 
  - First Model: Linear Regression
    - A linear regression model was built using a pipeline that combined preprocessed data and the model defined. The metrics (mainly the R-squared) on both the training and testing data suggest that the model is underfitted. The metrics are as follows: 
    -   Regression Metrics: Training Data
   -  MAE = 847.129
   -  MSE = 1,297,558.136
   -  RMSE = 1,139.104
   -  R^2 = 0.562
    -   Regression Metrics: Testing Data
   -  MAE = 804.120
   -  MSE = 1,194,349.715
   -  RMSE = 1,092.863
   -  R^2 = 0.567


- Visualizing Linear Regression Coefficients:
   <img width="710" height="435" alt="coef" src="https://github.com/user-attachments/assets/6fb8daa7-5c5b-4ddd-aaea-1eb9f29f3b61" />

The model predicts baseline sales of about 1,900 units and shows that higher-priced items tend to sell more. Outlet type also matters, with grocery stores generally seeing lower sales than other outlets. These insights highlight which products and stores drive overall sales, supporting data-driven decisions.








- Second Model: The Random Forest Model (Recommended)

    - The Random Forest model is recommended as the final model due to its superior predictive performance and better generalization compared to the linear models.
   - The model achieves an R² of approximately 0.60 on test data, meaning it explains about 60% of the variability in Item_Outlet_Sales.
   - The MAE is around 700 units, which is acceptable given that:
      - The average sales value is ~2,200 units
      - The maximum sales value exceeds 13,000 units, this indicates that the model’s prediction error is reasonable relative to the scale of the target variable.

   - R² Interpretation (Non-Technical) :
     - The Random Forest model explains about 60% of the uncertainty in product sales. The remaining 40% is influenced by external factors such as promotions, customer behavior, and store-specific conditions that are not captured in the dataset.

   - Overfitting / Underfitting Analysis
     - Training R² ≈ 0.69, Test R² ≈ 0.60
     - The moderate gap between training and test performance indicates controlled overfitting.
     - The model generalizes well but is not perfectly fitted, likely due to missing key predictors rather than insufficient model complexity.

 -  The metrics for the Tuined Model are:
     - Regression Metrics: Training Data
       - MAE = 664.034
       - MSE = 896,591.868
       - RMSE = 946.885
       - R^2 = 0.697

     - Regression Metrics: Testing Data
      - MAE = 734.312
      - MSE = 1,099,779.311
      - RMSE = 1,048.704
      - R^2 = 0.601

       
- Conclusion
  - The Random Forest model provides a balanced trade-off between accuracy and generalization, making it the most reliable choice for this dataset. Further improvements would require additional relevant features rather than a more complex model.

- Recommendations
 - There could be more advanced feature engineering to reorganize the features and capture hidden patterns that influence the target variable.


- Limitations
   - The dataset does not include external factors such as promotions, holidays, seasonality, or customer behavior, which likely explain part of the remaining unexplained variance.
   - The dataset does not contain a time variable, so the model predicts sales based on static features rather than capturing trends, seasonality, or time-based patterns.
  
