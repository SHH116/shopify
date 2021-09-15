# shopify


Python answer:
a)two of the stores have very skewed data. store with shop_id of 42 has unusually large total_items and order_amount. the store
with ship_id of 78 however has unusually large order_amount but not a correspondingly large total_items. given that all stores sell
affordable sneakers, the data of the latter store is totally meaningless and must be removed, but we are not cetain about how 
reliable the store 42 data is. So, we might keep that on.

b)Since the data is heavilty skewed instead of mean, we apply median outputing $284 per order . In addition, I have introduced 3 other metrics
to compare stores performance against each other from different angles:

1) answers how much bulk revenue per store was generated per week. 
2) answers how much volume each store sells per week
3) answers if customer base for a particular store is large or not. The larger the better. Remember this is an affordable item and
the more purchasers a particular store can target the better 

c)our new metrices are less prone to skewed data. For example, weekend sales Vs regular weekdays might carry some shocks/seasonalities,
which now are properly smoothed. The original AOV would average all the order_amount and hence hiding outlier/underperformer/outperformer stores
whereas now peer-to-peer comparison is much easier. Not only we know which stores are slackers, we also know in what dimension they need improvements.
SQL:

a: 4366

SELECT orderid,sum(quantity) FROM [OrderDetails]
WHERE orderid in (SELECT orderId FROM orders WHERE shipperid=3)


b: Peacock


SELECT od.orderid,sum(quantity) total,o.employeeid from orderdetails od
join orders o
on od.orderid=o.orderid
group by o.employeeid
order by total desc



c:Boston Crab Meat


SELECT productid, sum(quantity) total FROM [OrderDetails] od
join orders o
on od.orderid=o.orderid
Join Customers c
on c.customerid=o.customerid
where country ="Germany"
group by productid
order by total desc
