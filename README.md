# Telecom - Customer Churn End-to-End (Predictive ML + Production Deployment) | Risk Segmentation & Retention Optimization

---

## **Quick Section Summary**

- **Business Problem**
- **Objectives**
- **Technical Stack** 
- **Project Features**
- **Start-to-end pipeline**
- **Repository Structure**
- **Dashboard Snapshots**
- **Top 10 Churn Reasons and Recommended Solutions to Sales, Marketting and Leadership teams to Reduce Churn significantly**

---

## **Why This Project**
This project demonstrates an end-to-end ML deployment: **data → model → API → containerized service.**
It’s built for real-world decisioning (risk segmentation, retention revenue estimation, actionable reasons per customer).
It reflects a practical, business-focused approach to applying analytics for real-world impact in the **Telecom industry.**


## **Business Problem**

Telecom providers face persistently high customer churn, often exceeding 25%, which directly impacts recurring revenue and increases customer acquisition costs.
Churn behavior varies widely across customer segments based on tenure, contract type, and service usage, however sales & marketing teams lack timely, data-driven signals to intervene before customers leave.
Without predictive insight into who is at risk and why, retention campaigns remain reactive and inefficient, resulting in missed opportunities to protect revenue and improve customer lifetime value.


## **Objectives**

- Predict customers who are likely to churn using historical data.
- Analyze churn patterns across age, gender, state, services, contract type, and more.
- Deliver actionable insights via a Power BI dashboard.
- Enable marketing and sales teams to track churn KPIs in real time.


## **Technical Stack**

Power BI (DAX, Power Query), Python (Pandas, NumPy, Scikit-learn), SQL, Random Forest / XGBoost, Jupyter Notebook, FastAPI, Docker.

---
# **Project Features**

**“I intentionally kept the ***Power BI dashboard and the churn prediction API decoupled.***
This ensured demo reliability, avoided unnecessary cloud costs, and kept the architecture clean.
If required, the API can be integrated into Power BI using DirectQuery or REST.”**

- **Layer 1:** Power BI — insight discovery & business storytelling
- **Layer 2:** API — production-grade ML inference

- Built an end-to-end churn solution combining data analysis, predictive modeling, an interactive Power BI dashboard, and a deployed REST API for real-time churn prediction.
- A Dockerized FastAPI service that loads a trained Random Forest churn model, returns batch predictions with probabilities, risk levels, business summary metrics, and human-readable key factors.
- Model trained offline (Jupyter) → artifacts saved → FastAPI loads artifacts → Docker container serves REST endpoint → Swagger / PowerShell / Power BI call the endpoint for live scoring.
   - **Batch inference**  via `/predict` (accepts multiple customer records)
   - **Per-customer:** prediction, probability, risk level, and key factors
   - **Business summary:** churn rate, churn count, retention revenue potential
   - Swagger UI documentation (auto-generated)
   - Dockerized for easy local or cloud deployment



## **Start-to-end pipeline (concise steps)**
1. **Data collection** — gather raw customer/usage, billing, and interaction data.  
2. **Exploration & cleaning** — EDA, missing value handling, consistent naming, save training snapshot.  
3. **Feature engineering** — tenure, averages, contract flags, payment method encodings.  
4. **Train & validate** — model selection (Random Forest), cross-validation, calibration if needed.  
5. **Save artifacts** — model (`.pkl`), encoders, feature list, metadata.  
6. **Build service** — FastAPI `predict` endpoint with safe preprocessing.  
7. **Containerize** — Dockerfile + build image.  
8. **Local test** — Swagger, PowerShell, batch requests.  
9. **Deploy** — API using FastAPI + Docker



## **Repository Structure**
```
telecom-churn/
├── api/
│ ├── main.py # FastAPI app (predict endpoint)
│ ├── requirements.txt
├── data/
│ ├── 01_raw_source/customer_data_original.csv
│ └── 02_current_input/PredictionData.xlsx
├── python/
│ └── churn_ml_model.ipynb # training & preprocessing
│ └── score.py
├── model/
│  ├── churn_model.pkl
│  └── label_encoders.pkl
├── Dockerfile
```


---

# **Dashboard Snapshots**

###  Dashboard Summary
#### Created multiple pages:
  - **1.Summary Dashboard**: High-level KPIs (Churn %, Customer Count, Joiners)
  - **2. Prediction Dashboard**: Predicted Churners with filters and breakdowns
#### Used DAX measures, slicers, and drill-through filters to explore:
  - Churn by State, Age, Gender, Contract, Payment Type, Services
  - Churn by Category (e.g., Competition, Price, Dissatisfaction)

![Churn Analysis Summary_1](https://github.com/user-attachments/assets/6a693308-3202-4598-9272-b8fa56bcf756)

**(A high-level Page 1 summary)**

- Top Summary Box: Shows basics—6,418 total customers, 411 new joiners, 1,732 churned (27% rate).
- Gender Pie: Males (64%) churn more than females (36%).
- Age Bars: 20-35 year-olds have the highest churn (31%); under-20s are lowest.
- State Bars: Top churn states: Jammu (57%), Assam (38%), Jharkhand (35%).
- Internet Type Bars: Fiber optic users churn most (41%); none/low users least(8%).
- Payment & Contract Bars: Mailed checks (38%) and month-to-month contracts (47%) drive high churn.
- Services Table: Users with phone service (91%) or internet (93%) churn less if they have them.
- Churn Reasons Bars: Competition causes most (44%); price least (11%).
- Prediction Side: Flags 376 at-risk customers; profiles show mostly females (65%), short-tenure (month-to-month 94%), in states like Uttar Pradesh.



![Churn Analysis Prediction_2](https://github.com/user-attachments/assets/7beef630-e2f8-4ef9-a2ca-e084234c7cee)

**(A high-level Page 2 summary of key churn findings)**

- The overall customer churn rate is **27%.**
- Older customers (50+) and those on month-to-month contracts are most at risk.
- Jammu & Kashmir, Assam, and Jharkhand show the highest churn percentages.
- Lack of services like **Device Protection**, **Online Security**, and **Premium Support** was common among churners.
- **Mailed Check payment** users churn more frequently than Credit Card users.
- Customers with **Fiber Optic connections** and multiple services have higher churn likelihood.
- **Young adults (20-35)** in high-churn states on fiber and month-to-month plans drop fastest—these should be prioritized for retention.
- Not having device protection services increases churn risk by **30-40%.**
- **44%** of churners leave for competitors, highlighting the importance of attractive bundles.




### Relationship Table Mapping
![Mapping_Tables](https://github.com/user-attachments/assets/1baf0c78-1b38-4af8-8342-fa5e1b82e84b)

---


# **Top Churn Reasons and Recommended Solutions**
## **Top 10 Churn Reasons:**
### Sorted by Impact Priority

- **High Monthly Charges:** Customers paying higher-than-average fees often leave due to perceived lack of value or pricing dissatisfaction.
- **Month-to-Month Contracts:** Customers on short-term, flexible plans are more likely to churn compared to annual or two-year contracts.
- **Low Tenure / New Customers:** Newer customers (0–12 months) are more likely to churn, often due to unmet expectations or poor onboarding.
- **Multiple Complaints or Support Calls:** High interaction with customer support (especially unresolved issues) often correlates with dissatisfaction and churn.
- **Service Downtime / Technical Issues:** Repeated service failures or outages lead to frustration and switching.
- **Lack of Add-On Services:** Churn is higher among customers not using services like online backup, tech support, or security features.
- **No Internet Service / DSL Users:** Customers not using internet services or using slower options (like DSL) tend to churn more than fiber users.
- **Senior Citizen Segment:** This demographic may show higher churn depending on digital literacy, support needs, or service relevance.
- **Lack of Loyalty Incentives:** Absence of targeted offers, discounts, or retention strategies contributes to early exits.
- **No Paperless Billing or AutoPay:** Indicates lower engagement or trust, often a churn signal.



# Top 10 Recommended Solutions to Sales, Marketting and Leadership teams to Reduce Churn significantly:
### Sorted by Impact Priority

- **Target At-Risk Segments Proactively:** Use churn risk scores to send retention offers or personalized support to high-risk customers.
- **Promote LongTerm Contracts:** Offer discounts or loyalty perks for customers who switch from month-to-month to 1- or 2-year plans.
- **Upsell Value-Add Services:** Bundle services like online security, tech support, or streaming to increase stickiness and engagement.
- **Improve Onboarding for New Customers:** Implement welcome programs, personalized setup guides, and first-30-day follow-up calls to reduce early churn.
- **Enhance Service Quality for DSL Users:** Migrate legacy customers to higher-speed options like fiber with promotional pricing or device upgrades.
- **Reward Loyalty:** Implement rewards, referral bonuses, or exclusive discounts for long-term, low-complaint customers.
- **Reduce Support Friction:** Improve first-call resolution and reduce wait times; invest in AI chatbots or self-service tools.
- **Introduce Tiered Pricing Models:** Align pricing with usage patterns and customer segments to provide more value at lower perceived cost.
- **Monitor and Act on Feedback:** Regularly review NPS, CSAT, and complaint data; close the loop with customers when issues are resolved.
- **Incentivize Paperless Billing and AutoPay:** Offer small credits or priority support to customers who switch to these options (shows commitment).


##  **How to run**

1. Clone the repo or download as ZIP.
2. Open the `.pbix` file in Power BI Desktop to explore the dashboard.
3. Open `telecom_churn_model.ipynb` in Jupyter to review or retrain the ML model.
4. Check SQL folder for the views used in ETL processing.


---

# Author

### **Shaik Mayeenuddin**
***Aspiring Data Scientist Professional | Supply Chain & Marketing Analytics Expert Pursuing a Master’s in Data Science (AI & ML) Student***
🔗 https://www.linkedin.com/in/shaikmayeenuddin


 This project is built upon the foundational work by **Pivotalstats** . 
 I am grateful for the analytical insights shared through their tutorials
