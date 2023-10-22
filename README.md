# Pizza_Sales_SQL

-- Used UNION, SUBQUERY, AGGREGATED functions to analyze the Pizza sales.

select * from Pizza_Sales;

select sum(unit_price) as Total_Unit_Price from Pizza_Sales;

Select Sum(total_Price) as Total_Total_Price from Pizza_sales;

select Pizza_Name, Quantity from Pizza_Sales order by Quantity desc;

-- 

select Total_Price_Cal - Total_Price as Diff from (
select Quantity*Unit_Price as Total_Price_Cal, Total_Price from Pizza_Sales) as a order by Diff desc;

-- Pizza Category Total Revenue

select distinct Pizza_Category from Pizza_Sales;

select pizza_category, round(sum(total_price),0) as Total_Category_Price, round(sum(quantity),0) as Total_Quantity_Category from pizza_Sales group by Pizza_Category order by Total_Category_Price;

-- Average cost spend on each category

select pizza_category, Total_Sales, Avg_Order, Avg_Order_Price, round(total_category_Price/Total_Quantity_Category, 0) as Average_Price_Category from (
select pizza_category,round(sum(total_price)*100 / (select sum(total_price) from pizza_sales), 0) as Total_Sales, sum(quantity)*100 / (select count(distinct order_id) from Pizza_Sales) as Avg_Order, round(sum(Total_price)/ count(distinct order_id), 0) as Avg_Order_Price, round(sum(total_price),0) as Total_Category_Price, round(sum(quantity),0) as Total_Quantity_Category from pizza_Sales group by Pizza_Category) as a;

-- Pizza Size Total Revenue

select distinct Pizza_size from Pizza_Sales;

select pizza_size,round(sum(Total_price)/ count(distinct order_id), 0) as Avg_Order_Price ,round(sum(total_price),0) as Total_size_Price, round(sum(Quantity),0) as Total_Quantity_Siz from pizza_Sales group by Pizza_size order by Total_size_Price;

-- Average cost spend on each pizza size

select Pizza_Size, Total_sales, Avg_Order, Avg_Order_Price, round(Total_size_Price/Total_Quantity_Siz,0) as Average_Size_Price from (
select pizza_size, round(sum(total_price)*100 / (select sum(total_price) from pizza_sales), 0) as Total_Sales, sum(quantity)*100 / (select count(distinct order_id) from Pizza_Sales) as Avg_Order, round(sum(Total_price)/ count(distinct order_id), 0) as Avg_Order_Price, round(sum(total_price),0) as Total_size_Price, round(sum(Quantity),0) as Total_Quantity_Siz from pizza_Sales group by Pizza_size) as a;

-- Pizza's being sold

select pizza_name, sum(quantity) / count(distinct order_id) as Avg_Order, round(sum(Total_price),0) as Pizza_Revenue, round(sum(quantity),0) as Total_Quantity from Pizza_sales group by pizza_name order by Pizza_Revenue;

-- Average cost spend on each different pizza

select Pizza_name,Total_Sales, Avg_Order, Avg_Order_Price, round(Pizza_revenue/Total_Quantity,0) as Average_Pizza_Cost from (
select pizza_name, round(sum(total_price)*100 / (select sum(total_price) from pizza_sales), 0) as Total_Sales ,sum(quantity) / count(distinct order_id) as Avg_Order, round(sum(Total_price)/ count(distinct order_id), 0) as Avg_Order_Price, round(sum(Total_price),0) as Pizza_Revenue, round(sum(quantity),0) as Total_Quantity from Pizza_sales group by pizza_name) as a order by Average_Pizza_Cost desc;

-- Total Pizzas sold

select sum(Quantity) as Total_Sold from Pizza_Sales;

select round(sum(Total_price)/ count(distinct order_id), 0) as Avg_Order_Price from Pizza_Sales;

select count(distinct order_id) as Total_orders from Pizza_Sales;

select sum(quantity) / count(distinct order_id) as Avg_Order from Pizza_Sales;

select order_date, count(distinct order_id) as Orders from pizza_sales group by order_date;

select datename(DW, order_date) as order_day, count(distinct order_id) as Orders from pizza_sales group by datename(DW, order_date) order by Orders desc;

select datename(month, order_date) as order_month, count(distinct order_id) as Orders from pizza_sales group by datename(month, order_date) order by Orders desc;

select datename(year, order_date) as order_year, count(distinct order_id) as Orders from pizza_sales group by datename(year, order_date) order by Orders desc;

select * from Pizza_Sales;

select datename(hour, order_time) as order_time, count(distinct order_id) as Orders from pizza_sales group by datename(hour, order_time) order by Orders desc;

select pizza_category, round(sum(total_price)*100 / (select sum(total_price) from pizza_sales), 0) as Total_Sales from Pizza_Sales group by pizza_category;

select pizza_category, round(sum(total_price),0) as Total_Sales, round(sum(total_price)*100 / (Select sum(total_price) from pizza_sales where month(order_date) = 1),0) as Total_Price
from Pizza_sales where month(order_date) = 1 group by pizza_category;

select pizza_size, round(sum(total_price),0) as Total_Sales, round(sum(total_price)*100 / (Select sum(total_price) from pizza_sales where datepart(quarter, order_date) = 1),0) as Total_Price
from Pizza_sales where datepart(quarter, order_date) = 1 group by pizza_size;

select Top 10 pizza_name, round(sum(total_price),0) as Total_Revenue from Pizza_Sales group by Pizza_name order by Total_Revenue desc;

select Top 10 pizza_name, round(sum(total_price),0) as Total_Revenue from Pizza_Sales group by Pizza_name order by Total_Revenue asc;

select * from (select Top 5 pizza_name, round(sum(total_price),0) as Total_Revenue from Pizza_Sales group by Pizza_name order by Total_Revenue desc) as a
union 
select * from (select Top 5 pizza_name, round(sum(total_price),0) as Total_Revenue from Pizza_Sales group by Pizza_name order by Total_Revenue asc) as b;

select Top 10 pizza_name, count( distinct order_id) as Total_Quantity from Pizza_Sales group by Pizza_name order by Total_Quantity desc;

select Top 10 pizza_name, count( distinct order_id) as Total_Quantity from Pizza_Sales group by Pizza_name order by Total_Quantity asc;

select * from (select Top 5 pizza_name, count( distinct order_id) as Total_Orders from Pizza_Sales group by Pizza_name order by Total_Orders desc) as a 
union
select * from (select Top 5 pizza_name, count( distinct order_id) as Total_Orders from Pizza_Sales group by Pizza_name order by Total_Orders asc)as b;

select Top 5 pizza_name, sum(quantity) as Total_Pizzas from Pizza_Sales group by Pizza_name order by Total_Pizzas desc

select Top 5 pizza_name, sum(quantity) as Total_Pizzas from Pizza_Sales group by Pizza_name order by Total_Pizzas asc

select * from (select Top 5 pizza_name, sum(quantity) as Total_Pizzas from Pizza_Sales group by Pizza_name order by Total_Pizzas desc) as a 
union
select * from (select Top 5 pizza_name, sum(quantity) as Total_Pizzas from Pizza_Sales group by Pizza_name order by Total_Pizzas asc)as b;
