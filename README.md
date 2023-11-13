
>1. Can models trained using Random Forests overfit?

Yes, models trained using Random Forests can potentially overfit, although Random Forests are designed to mitigate overfitting compared to individual decision trees. Random Forests work by training multiple decision trees on different subsets of the data and then averaging their predictions. This ensemble approach helps reduce overfitting because the individual trees may overfit to different subsets, and their combined prediction tends to be more robust.

However, there are situations where a Random Forest can still overfit. For example, if the individual trees in the forest are allowed to grow too deep, they may overfit to the training data. Similarly, if the individual trees are allowed to have too few samples in each leaf node, they may overfit to the training data. In general, the more complex the individual trees in the forest are, the more likely the Random Forest is to overfit.



>2. Please, calculate the 80th percentile of the turnover of all organizations based in London or New York that had a loan open in the last 30 days with an amount lower than 1000 USD.

```sql
select 
    percentile_cont(0.8) within group (order by c.stated_turnover)
from 
    clientdata c
join 
    open_loans ol on c.id = ol.client_id
where 
    (c.city = 'London' or c.city = 'New York') and 
    ol.amount_granted < 1000 and
    ol.requested_at >= now() - interval '30 days'
```
