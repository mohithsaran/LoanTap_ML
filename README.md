## **LoanTap**



#### **Introduction**
Loantap is a leading financial technology company based in India, specializing in providing flexible and innovative loan products to individuals and businesses. With a focus on customer-centric solutions, Loantap leverages technology to offer hassle-free borrowing experiences, including personal loans, salary advances, and flexible EMI options. Their commitment to transparency, speed, and convenience has established them as a trusted partner for borrowers seeking efficient financial solutions.

- LoanTap is at the forefront of offering tailored financial solutions to millennials.

- Their innovative approach seeks to harness data science for refining their credit underwriting process.

- The focus here is the Personal Loan segment. A deep dive into the dataset can reveal patterns in borrower behavior and creditworthiness.

- Analyzing this dataset can provide crucial insights into the financial behaviors, spending habits, and potential risk associated with each borrower.

- The insights gained can optimize loan disbursal, balancing customer outreach with risk management.

#### **Problem Statement**
LoanTap is an online platform committed to delivering customized loan products to millennials. They innovate in an otherwise dull loan segment, to deliver instant, flexible loans on consumer friendly terms to salaried professionals and businessmen.

The data science team at LoanTap is building an underwriting layer to determine the creditworthiness of MSMEs as well as individuals.

LoanTap deploys formal credit to salaried individuals and businesses 4 main financial instruments:

- Personal Loan
- EMI Free Loan
- Personal Overdraft
- Advance Salary Loan

This case study will focus on the underwriting process behind Personal Loan only

- Dataset link: https://drive.google.com/file/d/1Eky6bPeveLFia9LFo1iXv_SBf21HXW5P/view?usp=sharing

#### **Dataset Features**
- `loan_amnt` : The listed amount of the loan applied for by the borrower. If at some point in time, the credit department reduces the loan amount, then it will be reflected in this value.
- `term`: The number of payments on the loan. Values are in months and can be either 36 or 60.
- `int_rate` : Interest Rate on the loan
- `installment` : The monthly payment owed by the borrower if the loan originates.
- `grade` : LoanTap assigned loan grade
- `sub_grade` : LoanTap assigned loan subgrade
- `emp_title` :The job title supplied by the Borrower when applying for the loan.*
- `emp_length` : Employment length in years. Possible values are between 0 and 10 where 0 means less than one year and 10 means ten or more years.
- `home_ownership` : The home ownership status provided by the borrower during registration or obtained from the credit report.
- `annual_inc`: The self-reported annual income provided by the borrower during registration.
- `verification_status` : Indicates if income was verified by LoanTap, not verified, or if the income source was verified
- `issue_d` : The month which the loan was funded
- `loan_status` : Current status of the loan - Target Variable
- `purpose` : A category provided by the borrower for the loan request.
- `title` : The loan title provided by the borrower
- `dti` : A ratio calculated using the borrower’s total monthly debt payments on the total debt obligations, excluding mortgage and the requested LoanTap loan, divided by the borrower’s self-reported monthly income.
- `earliest_cr_line` :The month the borrower's earliest reported credit line was opened
- `open_acc` : The number of open credit lines in the borrower's credit file.
- `pub_rec`: Number of derogatory public records
- `revol_bal` : Total credit revolving balance
- `revol_util` : Revolving line utilization rate, or the amount of credit the borrower is using relative to all available revolving credit.
- `total_acc` : The total number of credit lines currently in the borrower's credit file
- `initial_list_status` : The initial listing status of the loan. Possible values are – W, F
- `application_type` : Indicates whether the loan is an individual application or a joint application with two co-borrowers
- `mort_acc` : Number of mortgage accounts.
- `pub_rec_bankruptcies` : Number of public record bankruptcies
- `Address: Address of the individual
  
#### After Performing SMOTE on Logistic Regression
![image](https://github.com/user-attachments/assets/52e4c604-854c-4821-b02d-897fe131a15f)
- Accuracy: 0.8335479635381158
- Precision Score: 0.5596133725275273
- Recall Score: 0.7210631058612056

#### After Hyperparameter tuning
- Precision: 0.86
- Recall: 0.84
- F1-Score: 0.84
- ROC-AUC: 0.90

 **Tradeoff Questions**:
    - How can we make sure that our model can detect real defaulters and there are less false positives? This is important as we can lose out on an opportunity to finance more individuals and earn interest on it. 
    
        - By increasing the prediction threshold (e.g., from 0.5 to 0.7), only borrowers with a very high likelihood of default will be flagged as defaulters.
        
        - Set stricter approval criteria for high-risk borrowers based on model predictions.     Offer secured loans or reduced credit limits to mitigate risk.
        
        - Risk: High recall may result in rejecting creditworthy borrowers, leading to lost business.
        
        - Benefit: Safeguards against NPAs, reducing long-term financial risks.
        
    - Since NPA (non-performing asset) is a real problem in this industry, it’s important we play safe and shouldn’t disburse loans to anyone.
        - Combine precision and recall to find a balanced model performance.
        
        - Use the ROC-AUC and Precision-Recall curves to identify optimal thresholds that balance both metrics.
        
**Additional Questions:**
    - What percentage of customers have fully paid their Loan Amount?
    
      - `80.38%` has fully paid the loan
      
    - Comment about the correlation between Loan Amount and Installment features.
    
      -The correlation coefficient measures the strength and direction of the linear relationship between two variables. In this case, the correlation coefficient between 'loan_amnt' and 'installment' is quite high, approximately 0.95, indicating a strong positive linear relationship between these two variables.
      
      - Loan Terms: Understanding the relationship between loan amount and installment payments is crucial for setting appropriate loan terms. Lenders can adjust loan terms such as interest rates and repayment periods based on the borrower's ability to handle installment payments associated with different loan amounts.
      
      - Potential Multicollinearity: When building predictive models, it's essential to be cautious of multicollinearity between highly correlated predictor variables. Multicollinearity can lead to unstable estimates and difficulties in interpreting the model coefficients. Therefore, it might be necessary to address multicollinearity through techniques such as variable selection or regularization.
      
    - The majority of people have home ownership as `Mortgage`
    
    - People with grades ‘A’ are more likely to fully pay their loan. 
    
      - `True`. **Grade 'A' borrowers demonstrate a significantly high likelihood of fully repaying their loans**, with True. Grade 'A' borrowers demonstrate a significantly high likelihood of fully repaying their loans, with approximately **93.71%** of loans being fully paid. 
      
      - This suggests that borrowers with the **highest credit rating** are more inclined to fulfill their loan obligations successfully. of loans being fully paid. This suggests that borrowers with the highest credit rating are more inclined to fulfill their loan obligations successfully.
      
    - Name the top 2 afforded job titles.
    
    - The Most afforded job titles are Teachers & Managers.
      

- Thinking from a bank's perspective, which metric should our primary focus be on..
1. ROC AUC
2. Precision
3. Recall
4. F1 Score

- From a bank's perspective, minimizing risks and maximizing profitability are paramount. ROC AUC (Receiver Operating Characteristic Area Under Curve) is indeed a crucial metric because it encompasses both True Positive Rate (TPR) and False Positive Rate (FPR)

- Bank's primary focus should be on ROC AUC , because bank needs to reduce FPR (False Positive Rate) and needs to increase the TPR (True Positive Rate).
    Maximizing TPR ensures that the bank correctly identifies customers who fully pay their loans (reducing False Negatives), while minimizing FPR ensures that the bank doesn't wrongly classify customers as fully paid when they're actually charged off (reducing False Positives).

- By optimizing ROC AUC, the bank can strike a balance between correctly identifying creditworthy customers and minimizing the risk of defaulters, thereby enhancing the overall performance and reliability of its credit scoring model.

- How does the gap in precision and recall affect the bank?

    - To comprehend the errors made by a model, it's crucial to evaluate both false positives and false negatives, which are gauged through metrics like recall and precision. When recall is low, it poses a significant risk for the bank.
    - So, the gap between precision and recall will affect the bank. As the gap widens, there will be increase in incorrect predictions.
    - Good precision means less False Positives. i.e. Less NPA loan accounts.
    - Good recall means less False Negatives. i.e. not loosing on good customer.
 
- Which were the features that heavily affected the outcome?
    - `loan_amnt`, `int_rate`, `dti`, `open_acc`, `revol_util` are the features that affects the outcome heavily
- Will the results be affected by geographical location? (Yes/No)
    - Yes, we can see that zip_code (Address) is a very important feature so geographical location has impact on our result.
    
- Focus on maximizing the F1 score and area under the Precision-Recall Curve to effectively manage the precision-recall trade-off. This ensures identifying most defaulters while reducing false positives, enhancing risk management.
- Consider using more complex classifiers like Random Forests or XGBoost and perform hyperparameter tuning to enhance model performance and capture intricate relationships in the data.
- Employed stratified k-fold cross-validation to ensure representative distribution of minority class in each fold, providing reliable estimates of model performance.
- Optimize Loan Approval Strategy:

    - Scrutinize loans with lower grades more rigorously and consider adjusting interest rates to compensate for higher risk.
    - Implement targeted strategies for high-risk zip codes, such as additional verification steps or higher interest rates.
    - Evaluate small business loans with additional financial health checks and collateral requirements to mitigate default risk.
    - By implementing these recommendations, LoanTap can enhance their loan approval process, minimize the risk of NPAs, and ensure sustainable growth and financial stability.

#### **Conclusion**
- The Logistic Regression model for LoanTap demonstrates significant predictive power with a precision of 86% and an accuracy of 84%. The adjustments made to the threshold successfully enhanced precision, reducing the likelihood of false positives. These results suggest that the model is well-suited for LoanTap's operational needs in assessing loan risk and informing decision-making.

