# Supermarket Campaign Analysis 🛒

## Overview
This project looks at customer data from a supermarket to try and predict who is actually going to respond to marketing campaigns. 

Usually, companies just send promotional material to everyone. In our dataset, only about 15% of people actually responded to the last campaign. Sending offers to the other 85% is basically throwing marketing budget out the window. This project explores how we can use machine learning to get smarter about who we target.

---

## What the Data Tells Us (EDA)
Before getting into the predictive modeling, I took a look at the data to see what naturally drives customer behavior. A few interesting things stood out:

* **Window Shoppers vs. Buyers:** High website traffic doesn't automatically mean high sales. A lot of high-frequency visitors are just browsing.
* **The "Kidhome" Factor:** Households with more kids at home make way fewer in-store purchases. It makes more sense to target these families with web or catalog campaigns.
* **Campaign Synergy:** Customers who engage with one campaign are highly likely to engage with another. Once someone responds, they are a great candidate for future retention campaigns.

---

## Preprocessing & Modeling
Real-world data is usually a bit messy, so I did some cleanup before feeding it into the models:
* Created dynamic features like customer age and tenure based on dates.
* Capped extreme outliers in income and spending so they wouldn't skew the results.
* Grouped continuous numerical data (like spending amounts) into ranked bins to help the models find clearer patterns.

Since only 15% of the data represented a positive response, I had to handle class imbalance (using SMOTE) to make sure the model didn't just lazily predict "No" for everyone. I tested out Logistic Regression, Random Forest, and Gradient Boosting to see which handled the data best.

---

## The Main Takeaway: Decile Analysis
The most important part of this project isn't just getting a model to predict "Yes" or "No" it's figuring out how to use those predictions in the real world. That is where **Decile Analysis** comes in.

Instead of a binary yes/no, the model outputs a *probability score* for each customer. I ranked the entire customer base by this score from highest to lowest, and split them into 10 equal groups (deciles). 

**Why does this matter?**
* **Decile 1 & 2 (The Top 20%):** These are the customers the model is most confident will respond. 
* **The Result:** By targeting *only* these top deciles, we can capture the vast majority of the actual campaign responders. 

Instead of spending money to reach 100% of the customer base, the marketing team can reach out to just the top 20% to 30%. They still get almost all of the conversions, but they spend a fraction of the cost, massively improving the Return on Ad Spend (ROAS) and avoiding spamming people who just aren't interested.

---

## How to Run the Code
If you want to run this analysis yourself:

1. Clone the repository to your local machine.
2. Make sure you have the necessary libraries installed (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`).
3. Open the Jupyter Notebook (`notebooks_Supermarket_Campaign_Analysis.ipynb`) and run the cells.
