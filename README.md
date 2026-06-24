# CUSTOMER-TRENDS-ANALYSIS-
This project presents a Customer Behavior Analysis that visualizes key metrics about customer demographics, purchasing behavior, and subscription status. It provides actionable insights into sales performance, revenue distribution, and customer preferences.
import pandas as pd
from google.colab import files
uploaded = files.upload()
df = pd.read_csv('customer_shopping_behavior.csv')
df.head()
df.info()
df.describe(include="all")
df.isnull().sum()
df["Review Rating"] = df.groupby("Category")["Review Rating"].transform(
    lambda x: x.fillna(x.median())
)
df.isnull().sum()
df.columns=df.columns.str.lower()
df.columns=df.columns.str.replace(' ','_')
df=df.rename(columns={'purchase_amount_(usd)':'purchase_amount'})
df.columns
# create a column age_group
labels=['Young Adults','Adult','Middle-aged','Senior']
df['age_group']=pd.qcut(df['age'],q=4,labels=labels)
df[['age','age_group']].head(10)
#create column purchase_frequency_days
frequency_mapping={
    'Fortnightly':14,
    'Weekly':7,
    'Monthly':30,
    'Quarterly':90,
    'Bi-Weekly':14,
    'Annually':365,
    'Every 3 Months':90
}
df['purchase_frequency_days ']=df['frequency_of_purchases'].map(frequency_mapping)
df[['purchase_frequency_days ', 'frequency_of_purchases']].head(10)
df[['discount_applied','promo_code_used']].head(10)
df['discount_applied']==df['promo_code_used'].all()
df=df.drop('promo_code_used',axis=1)
df.columns
<img width="1363" height="731" alt="image" src="https://github.com/user-attachments/assets/d38d061a-f7b5-4dc7-a0e6-e62149a894cb" />

