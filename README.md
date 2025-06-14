# Pizza_Sales_Analysis_SQL

![image](https://github.com/user-attachments/assets/8e2dd4b0-fe1d-4c91-be86-eab92f119ade)


Tools used : Excel,MS SQL Server,Power BI

Dataset used

SQL Analysis-code

Power BI Dashboard

Power BI Dashboard

Business Problem

A pizza company needs a robust and scalable data analytics solution to handle the vast amount of data(approximately 50k rows of data combined) to effectively analyze and extract meaningful insights like trends, order patterns, menu performance, customer preferences and other key business metrics. Visualizations must also be created to identify trends and insights related to daily and monthly order volume, sales by pizza type and size, and top/bottom sellers. The end goal is to equip the business with data-driven insights that inform strategic decisions to improve operations and profitability.

Solution Plan

1.In helping the pizza company gain valuable insights from their sales data CSV file, I will utilize SQL and data visualization with Power BI to extract relevant information and conduct insightful analyses. Data cleaning/processing, data transformation and analysis shall be done.

2.By leveraging SQL's functions, I can uncover key metrics like total revenue, average order size, and best/worst selling menu items.

3.Once the data has been extracted and prepared, I will leverage Power BI to present the findings through interactive visualizations. This will allow stakeholders at the pizza company to gain actionable insights into sales trends, order patterns, and menu performance through visually compelling charts, graphs, and reports.

4.I plan on creating a dynamic Power BI dashboard that enables users to explore details on daily order volume, sales by pizza type/size, or top/bottom selling items. The end goal is equipping the business with data-driven insights to inform strategic decisions that improve operations and profitability.

Execution

Questions Answered from the Dataset

1) What are the Key Performance Indicators obtained from the Dataset?

Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

![image](https://github.com/user-attachments/assets/9c673ba9-3529-489f-b360-1f42496e4837)

This metric provides a clear measure of the overall financial performance of the pizza sales. It indicates the total amount of money generated from pizza orders over a specific period, reflecting the revenue potential of the business.

Average Order Value:

  SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales

  ![image](https://github.com/user-attachments/assets/907df8da-9d88-4053-8209-1850858a451a)

  Average order value helps in understanding customer spending habits and the effectiveness of marketing strategies. A higher average order value indicates that customers are spending more per transaction, which can contribute to increased revenue and profitability.

Total Pizzas Sold:

  SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales

  ![image](https://github.com/user-attachments/assets/64806785-8643-48fa-8923-9c421d05ecd6)

  Total pizzas sold is a fundamental metric that directly reflects product demand. It provides insights into consumption patterns and helps in inventory management and production planning. Understanding total pizzas sold enables businesses to meet customer demand efficiently.

Total Orders:

  SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

  ![image](https://github.com/user-attachments/assets/0285e451-4c28-4e8a-87ef-09a160a61d05)

  Total orders represent the volume of transactions processed within a specific period. Tracking total orders helps in evaluating sales performance and identifying trends in customer behavior. It provides a basis for assessing business growth and operational efficiency.

Average Pizzas Per Order:

  SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
  CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
  AS Avg_Pizzas_per_order
  FROM pizza_sales

![image](https://github.com/user-attachments/assets/1845977e-82ef-414b-830f-dac9e2c89140)

Average pizzas per order indicates the average quantity of pizzas purchased in each transaction. This metric offers insights into customer preferences and ordering behavior. Higher average pizzas per order may indicate upselling opportunities or popular menu items.

2) Daily Trend for Total Orders

    SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
    FROM pizza_sales
    GROUP BY DATENAME(DW, order_date)

   ![image](https://github.com/user-attachments/assets/a1f6907a-d4fa-41e5-996e-f2e8ae855702)

   By analyzing the daily trend of total orders over a specific time period, we can identify patterns and fluctuations in order volumes on a daily basis. This helps in understanding the demand patterns throughout the week or month, enabling better inventory management and resource allocation.

3) Monthly Trend for Orders

    select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
    from pizza_sales
    GROUP BY DATENAME(MONTH, order_date)

   ![image](https://github.com/user-attachments/assets/25d0ade5-3cab-4277-80c9-33b7ae36318a)


   The monthly trend of total orders offers insights into the overall order activity throughout the month. Identifying peak periods of high order activity can aid in resource allocation, production planning, and promotional efforts. By recognizing monthly trends, businesses can adjust their operations to capitalize on high-demand periods and optimize efficiency during slower periods.

4) % of Sales by Pizza Category

    SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
    FROM pizza_sales
    GROUP BY pizza_category

   ![image](https://github.com/user-attachments/assets/792ede84-9a74-4c8f-a09b-6365e8c99aa0)


The distribution of sales across different pizza categories helps in understanding the popularity of each category and its contribution to overall sales. This insight informs menu optimization strategies, marketing campaigns, and inventory management decisions to maximize revenue and customer satisfaction.

5) % of Sales by Pizza Size

    SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
    FROM pizza_sales
    GROUP BY pizza_size
    ORDER BY pizza_size

   ![image](https://github.com/user-attachments/assets/56691cb0-94b2-4ee3-9d33-8c7e1d6f4964)

   The chart depicting the percentage of sales attributed to different pizza sizes provides insights into customer preferences regarding pizza size. Understanding these preferences allows for better inventory management and menu optimization to meet customer demand effectively.

6) Total Pizzas Sold by Pizza Category

    SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
    FROM pizza_sales
    WHERE MONTH(order_date) = 2
    GROUP BY pizza_category
    ORDER BY Total_Quantity_Sold DESC

   ![image](https://github.com/user-attachments/assets/a4e8286b-c686-4248-8e51-ac6e578c6ec8)

   The metric showing total number of pizzas sold for each pizza category enables comparison of sales performance across different categories. This visualization helps in identifying popular and less popular pizza options, informing marketing strategies and menu adjustments accordingly.

7) Top 5 Pizzas by Revenue

    SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Revenue DESC

   ![image](https://github.com/user-attachments/assets/96170e58-f584-4796-b82f-0988e9a193d5)

   The chart highlighting the top 5 best-selling pizzas based on revenue, total quantity, and total orders identifies the most popular pizza options. This insight aids in understanding customer preferences and allows for targeted promotions or menu enhancements to capitalize on high-demand items.

8) Bottom 5 Pizzas by Revenue

    SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Revenue ASC

   ![image](https://github.com/user-attachments/assets/922cf61c-4ecc-4613-9eb0-7313561826d9)

   Conversely, the chart showcasing the bottom 5 worst-selling pizzas based on revenue, total quantity, and total orders helps identify underperforming or less popular pizza options. This information is valuable for making strategic decisions such as discontinuing unpopular items or adjusting pricing and marketing strategies to boost sales.

9) Top 5 Pizzas by Quantity

    SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Pizza_Sold DESC
   ![image](https://github.com/user-attachments/assets/75454b82-b0d8-4653-b2f3-cf5593248a31)

   Identifying the top 5 pizzas by quantity sold provides insight into the most popular pizza varieties among customers. This information helps in understanding customer preferences and allows for targeted marketing efforts or menu optimizations to capitalize on high-demand items.

10) Bottom 5 Pizzas by Quantity

    SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Pizza_Sold ASC

    ![image](https://github.com/user-attachments/assets/059e0b53-3ebb-4019-9c82-ee05876fc364)

    Conversely, identifying the bottom 5 pizzas by quantity sold highlights less popular or underperforming pizza options. This insight can inform menu adjustments, promotional strategies, or inventory management decisions to minimize waste and maximize profitability.

11) Top 5 Pizzas by Total Orders

    SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Orders DESC

    ![image](https://github.com/user-attachments/assets/4863ba41-e370-44ed-a1f9-7b95be18cca9)


    Identifying the top 5 pizzas by total orders sheds light on the most frequently ordered pizza varieties. This information helps in understanding customer behavior and preferences, enabling businesses to tailor marketing campaigns and menu offerings to meet customer demand effectively.

12) Bottom 5 Pizzas by Total Orders

    SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
    FROM pizza_sales
    GROUP BY pizza_name
    ORDER BY Total_Orders ASC

    ![image](https://github.com/user-attachments/assets/578869f8-42ab-4859-9a47-185d94983436)

    Identifying the bottom 5 pizzas by total orders reveals less popular or niche pizza options that may require attention or adjustments. Understanding these trends allows businesses to make informed decisions regarding menu adjustments, promotional strategies, or inventory management to optimize sales and customer satisfaction.

13) Generated various Charts and Visuals on Power BI to identify trends/patterns and gain more insights into the data.

![image](https://github.com/user-attachments/assets/0da57a6e-dd80-4c7d-9980-ebb7d84e52c9)


![image](https://github.com/user-attachments/assets/2a427e74-b9e5-412f-bee9-22cf73236c98)


Conclusion
By delving into various facets of the pizza sales dataset, a comprehensive understanding of consumer behavior and market trends was attained. The analysis unveiled key insights, including the identification of peak and off-peak periods based on daily and monthly order trends. This knowledge equips businesses with the ability to optimize staffing and inventory management to meet varying demand levels effectively. Additionally, the examination of sales distribution across different pizza categories shed light on customer preferences, aiding in menu optimization and marketing strategies to enhance sales performance.

Moreover, calculating the average number of pizzas sold per order provided valuable insights into consumer behavior and consumption patterns, enabling businesses to tailor pricing strategies and portion sizes to maximize profitability and customer satisfaction. Overall, this analysis empowers the pizza establishment to make data-driven decisions, streamline operations, and enhance the overall customer experience, ensuring continued success in the competitive pizza market.












