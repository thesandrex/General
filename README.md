# Marketing-Analysis

## Project's description

We have 3 csv datasets from Yandex Afisha database (Yandex Afisha is the biggest russian prlatform created to aggregate tickets to different kind of actions like music festivals, cinemas, theaters and others).

Our data's describing period from june of 2017 to may of 2018 and contains:

1. Information about visits on the website;
2. Orders by the period;
3. Advertising costs statistics.


___Monetary units in form of USD.___

Our goal is to find the way how we can pull advertising costs down (refuse from non-benefitable traffic sources and redistribute the budget).

What should we define in our project:

1. How costumers use our platform;
2. When they usually make the first orders on the website;
3. How much each costumer brings to our company;
4. When costs for costumers attraction pay off.

## Metrics counting in project

* user activity metrics - dau, mau, wau;
* Average session duration - ASL;
* Retention Rate (cohort analysis is performed);
* Average check (cohort analysis is performed);
* "Lifetime" customer value (LTV) by "age" cohorts;
* Marketing costs by source;
* Cost of user engagement (CAC);
* ROMI by source.

## Visualisation in project

![Retention_Rate](https://i.ibb.co/P46R4kV/retentionrate.png "Retention Rate")

![AverageCheck](https://i.ibb.co/z4HMFXB/Average-Check.png "Average Check")

#### Cumulative LTV by lifetime cohorts
![LTV](https://i.ibb.co/1G91gMn/LTV.png "LTV")

## Lifetime cohorts estimate example

```python

#select activity month and first activity month

orders['activity_month'] = orders['buy_ts'].astype('datetime64[M]')
orders['first_activity_month'] = orders['first_activity_date'].astype('datetime64[M]')

#activity month take away first activity month equal lifetime period by month

orders['cohort_lifetime'] =(
    orders['activity_month'] - orders['first_activity_month']
)

orders['cohort_lifetime'] = ( 
    orders['cohort_lifetime'] / np.timedelta64(1, 'M')
)

orders['cohort_lifetime'] = orders['cohort_lifetime'].round().astype('int')

cohorts = orders.groupby(['first_activity_month', 'cohort_lifetime']).agg({'uid':'nunique'}).reset_index()

```

## Conclusion

As a result we got conclusions and recomendations for more effective use of advertising funds.
