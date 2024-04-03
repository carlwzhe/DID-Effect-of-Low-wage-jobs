# Machine Learning Enhancement of Minimum Wage Impact Analysis
## [The Effect of Minimum Wages on Low-wage Jobs](https://doi.org/10.1093/qje/qjz014)
Group members: Faye Yang, Lingfeng Shi, Nuha Alamri, Oscar Lu, Qijin Liu, Weizi He.

**Introduction:**

This repository contains a machine learning-based enhancement of the analysis originally presented in "The Effect of Minimum Wages on Low-Wage Jobs" by Cengiz, Dube, Lindner, and Zipperer (2019). The original study estimated the effect of minimum wages on employment using a difference-in-differences (DiD) approach across state-level minimum wage changes from 1979 to 2016. We build on this by addressing one of the main data challenges—missing values before DiD estimation.


Original Study Overview
The original research found that changes in the minimum wage did not lead to an overall loss of low-wage jobs. The study used a bunching estimator to assess the frequency distribution of wages and infer the impact on employment and earnings at the lower end of the wage distribution. They reported modest wage spillovers and no evidence of labor-labor substitution as a result of minimum wage changes.
Enhancements with Machine Learning


Handling Missing Data
Rather than using 0 to fill missing values as in the original approach, we employ a K-Nearest Neighbors (KNN) algorithm to predict and inpute these missing values, aiming for a more informed and accurate estimation base for DiD analysis.


Feature Importance
We utilize a Random Forest algorithm to determine the significance of various features on the impact of minimum wage changes. Specifically, we calculate the effect of minimum wage changes on different racial demographics, adding a weighted analysis pre-regression (Figure 1).


Results
Our machine learning-enhanced approach yields insights that were not fully apparent in the original paper. For instance, our results illustrate a distribution of estimated treatment effects (Figure 2) and an asymmetrical unimodal distribution, suggesting that effects are similar across most observational units.


Repository Structure
data_preprocessing/: Scripts for data cleaning and missing value imputation using **KNN**.
feature_analysis/: **Causal Random Forest models** to compute feature importance.


**Data:**

Original data: From replication backpack table 2, including CK_groups, state_panels_with3quant1979 and VZmw_quaterly_lagsleads_1979_2016.


Processed data: We split datasets CK_groups and state_panels_with3quant1979 by year. And using PreproT code to deal with VZmw_quaterly_lagsleads_1979_2016 to get the T variable using for the casual forest method.



**Methodology:** KNN and Casual Forest

**KNN Part:**

Our group divided the salary distribution based on race, gender, age, and other factors in various US states from 1979 to 2016 by year, then used KNN in machine learning to fill in the missing values, and then defined the feature variables (we chose year and quarter and state number statenum and some demographic characteristics as examples). Additionally, we assume that 'MW_real' is used directly as the treatment variable and 'emp' (employment number) as the outcome variable.

**Casual Forest Part:**

Data Preparation: The initial step involves loading and merging relevant datasets. Your example shows the merging of three datasets to form a final data frame, including demographic data (such as the population of black, white, gender-specific groups, and teenagers) along with other variables like state number and quarter dates.

Defining Variables:

Treatment Variable (T): In this case, the treatment variable seems to represent changes in the minimum wage, assumed to be MW_real. In practice, the treatment variable should signify the nature of the intervention or policy change, such as an increase in minimum wage.
Outcome Variable (Y): Here, it's represented by avewage, which could stand for average wage, indicating the effect of minimum wage changes on wages.
Covariates (X): These are the other variables that might influence the outcome aside from the treatment. In your example, demographic features like population by race, gender, and age groups are considered as covariates.
Causal Forest Implementation: With the EconML library's CausalForestDML class, a causal forest model is instantiated with gradient boosting regressors for both the outcome and treatment models. This approach allows for non-linear relationships and interactions between the covariates and the treatment effect on the outcome.

Model Fitting: The causal forest model is fitted using the defined variables. This process involves estimating the causal effect of the treatment on the outcome variable, controlling for the covariates.

Effect Estimation: After the model is fitted, you can estimate the treatment effects and visualize their distribution. This gives insights into how the treatment (e.g., changes in minimum wage) generally affects the outcome variable (e.g., average wages) across the dataset.

Feature Importance: An additional step involves evaluating the importance of each covariate in predicting the treatment effect. This can help identify which factors are most influential in determining how the treatment affects the outcome.

Visualization: The notebook includes steps for visualizing the distribution of estimated treatment effects and the feature importance scores. These visual representations aid in interpreting the model's findings and understanding the impact of different variables on the treatment effect.

**Colab link:**

KNN: https://colab.research.google.com/drive/1mK_u5fMY9Fk88L-Nk4OeooT8xLFVdRAu?authuser=1


Casual Forest: https://drive.google.com/drive/folders/1-qAhrif1STNy8GQkvQ1yuVe3SDfu_dhx?usp=drive_link
