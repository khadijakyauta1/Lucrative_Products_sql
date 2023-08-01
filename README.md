# Lucrative_Products_sql
analyzing the most lucrative products on facebook
 with lur as 
 (select product_id,
        sum(cost_in_dollars*units_sold) as total_revenue,
        rank() over (order by sum(cost_in_dollars*units_sold) desc) as qrank
from online_orders
where month(date) between 1 and 6
group by
    product_id)
select product_id, total_revenue
from lur
where qrank <=5
