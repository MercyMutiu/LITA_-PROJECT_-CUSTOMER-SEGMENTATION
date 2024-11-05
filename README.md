# LITA_-PROJECT_-CUSTOMER-SEGMENTATION
This shows the analysis of the customer data given for the LITA project

### Project Overview and Objective
Three different data analysis tools were used in the project. The project consists of the analysis of the customer data for a subscription service to identify the segments and trends.The goal is to know the customer behavior, track subscription types and identify thr trends in cancellations and renewals. Also the use of power BI dashboard to present the analysis.

### Data Sources
The dataset was provided by the facilitators for the final project of the data analysis class.

### Tools and Techniques
- Microsoft Excel:the use of pivot table to summarize the subscription pattern and the use of formulas to calculate the average and identify the most popular subscription
- SQL: different queries were written to gain insight on some of the questions asked.
- Power BI: a power BI dashboard was created to show the customer segment, cancellations and subscription trends.

### Steps Taken
1. Data Cleaning: The dataset was clened and the duplicates were removed making the rows reduce to 33788 rows
   -Pivot Table: the subscription pattern was summarized into a table.
![image](https://github.com/user-attachments/assets/50b4c982-3301-4ff8-afbc-e4efd6ac5a4b)
The image above shows the various tables created, one showing the subscription frequecy, subscription type, the sum of subscription and duration of subcription.
2. Data Analysis
 -Microsoft Excel was used to calculate the average subscription duration and to identify the most popular subscription type
   -Average subscription duration
   
   ```Excel
   =AVERAGE(I2:I33788)
   ```
   
   -Most popular subscription type
   
   ```Excel
   =COUNTIF(D2:D33788,"basic")
   ```
   
-SQL: Imported data from excel was converted to csv file. After that the null vales were removed before analysis

```SQL
delete from customerdata
where customer_id is null
```

-Retrieve the total number of customers from each region

```SQL
select region, count(distinct customerid) as TotalCustomers
from CustomerData
group by region
```

-Find the most popular subscription type by the number of customers

```SQL
select top 1
subscriptiontype, count(distinct customerid) as Customercount
from CustomerData
group by SubscriptionType
order by Customercount desc
```

-Find customers who canceled their subscription within 6 months

```SQL
select customerid, customer name
from CustomerData
where canceled = 1 and datediff(month, subscriptionstart, subscriptionend)<=6;
```

-Calculate the average subscription duration for all customers

```SQL
select AVG(datediff(month, subscriptionstart, subscriptionend)) as AvgSubDuration
from CustomerData
```

-Find customers with subscription longer than 12 months

```SQL
select customerid, customername
from CustomerData
where datediff(month, subscriptionstart, subscriptionend) > 12
```

-Calculate total revenue by subscription type

```SQL
select subscriptiontype, sum(revenue) as total revenue
from CustomerData
group by SubscriptionType
```

-find the top 3 regions by subscription cancellations

```SQL
select top 3 region, count(customerid) as cancellations
from CustomerData
where canceled =1
group by region
order by cancellations desc
```

-Find the total number of active and canceled subscription

```SQL
select sum(case when canceled = 0 then 1 else 0 end) as active subscriptions,
sum(case when canceled = 1 else 0 end) as canceledsubscriptions
from CustomerData
```
