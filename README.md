# Walmart-Data-Analysis-Supply-Chain.
## WALMART DATA ANALYSIS

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

train_df

train_df = pd.read_csv('train_walmart.csv')
stores = pd.read_csv('stores.csv')
features  = pd.read_csv('features.csv')

features.head()

stores.head()

train_df.isnull().sum()

stores.isnull().sum()

features.isnull().sum()

features.shape

features.drop(['MarkDown1', 'MarkDown2', 'MarkDown3', 'MarkDown4', 'MarkDown5'], axis=1,inplace=True)

features.fillna(method='ffill',axis=0,inplace=True)

features.isnull().sum()

## inner
df = train_df.merge(stores,how='inner',on=['Store'])

train_df.shape

df.shape

df.columns

features.columns

df = df.merge(features,how='inner',on=['Store','Date','IsHoliday'])

df

## date column in datetime - create new columns- year and week
df['Date'] = pd.to_datetime(df['Date'])


df['week'] = df.Date.dt.isocalendar().week

df['year'] = df.Date.dt.isocalendar().year

df

### write the function that can take feature name as input and create a scatter plot of that gicen feature and weekly sales

def scatter(column):
    plt.figure()
    plt.scatter(df[column],df['Weekly_Sales'])
    plt.ylabel('weekly_sales')
    plt.xlabel(column)

scatter('Store')

scatter('Size')

df.columns

scatter('Type')

################ line charts for weekly sales each year
###### avg weekly sales for the year 2012
x = df[df['year']==2010].groupby(['week'])['Weekly_Sales'].mean()
sns.lineplot(x.index,x.values,color='green')

y = df[df['year']==2011].groupby(['week'])['Weekly_Sales'].mean()
sns.lineplot(y.index,y.values,color='green')

z = df[df['year']==2012].groupby(['week'])['Weekly_Sales'].mean()
sns.lineplot(x=z.index,y=z.values,color='blue')

plt.figure(figsize=(20,10))
sns.lineplot(x.index,x.values,color='blue')
sns.lineplot(y.index,y.values,color='red')
sns.lineplot(z.index,z.values,color='green')
plt.grid()
plt.xticks(np.arange(1,60,step=1))
plt.legend(['2010','2011','2012'])
plt.xlabel('week',fontsize=16)
plt.ylabel('sales',fontsize=16)

sns.distplot(x=df['Weekly_Sales'],color='red')

############################ plot the stores with highest average sales
########################### plot the dept with hughest average sales


df

weekly_stores = df.groupby(['Store'])['Weekly_Sales'].mean().reset_index()

weekly_stores = weekly_stores.set_index('Store')

weekly_stores

weekly_stores.sort_values('Weekly_Sales').style.bar(align='left')

weekly_stores.values.reshape(-1,)

#### 
plt.figure(figsize=(25,12))
sns.barplot(weekly_stores.index,weekly_stores.values.reshape(-1,),palette='dark')
plt.grid()
plt.xlabel('store number',fontsize=16)
plt.ylabel('weekly_Sales',fontsize=16)
plt.title('weekly sales per store',fontsize=30)

###########
week_dept = df['Weekly_Sales'].groupby(df['Dept']).mean()

week_dept = pd.DataFrame(week_dept)

week_dept

week_dept.sort_values('Weekly_Sales',ascending=False).style.bar(align='left')

week_dept.values.reshape(-1,)

plt.figure(figsize=(25,12))
sns.barplot(week_dept.index,week_dept.values.reshape(-1,),palette='dark')
plt.grid()
plt.xlabel('dept',fontsize=16)
plt.ylabel('weekly_Sales',fontsize=16)
plt.title('weekly sales per department',fontsize=30)

plt.figure(figsize=(18,12))
sns.heatmap(df.corr(),annot=True)

df.columns

df.groupby(['Type'])['Weekly_Sales'].mean().plot(kind='bar')

#### 
sns.boxplot(x='Type',y='Size',data=df)

df.groupby(['year'])['Unemployment'].sum().plot(kind='bar')

df.groupby(['year'])['Weekly_Sales'].mean().plot(kind='bar')

df.groupby(['year'])['IsHoliday'].sum().plot(kind='bar')

df.groupby(['Dept'])['Unemployment'].sum()

df.groupby(['Dept'])['Unemployment'].sum().sort_values().head(10).plot(kind='bar')

df.groupby(['Dept'])['Unemployment'].sum().sort_values().tail(10).plot(kind='bar')
