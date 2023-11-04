# Brazil E-commerce Olist Business Analysis

## Introduction
Olist is an online retailer in Brazil that provides data on up to 100,000 orders on the internet. The aim of this analysis is to improve its business performance, particularly the Repurchase Rate, by exploring its datasets and providing actionable and specific recommendations.

## Data Sources and Used Tools
- Data Sources: Public Datasets from Olist
- Used Tools: Python (Pandas, Matplotlib, Numpy, NLTK), PostgreSQL, Power BI

## Relational Database in PostgreSQL
![olist_database](https://github.com/Fan287/olist_analysis/assets/148685693/0f2cab0e-e9f9-4fed-be98-9ec314b2e764)

## Dashboard in Power BI
![dashboard](https://github.com/Fan287/olist_analysis/assets/148685693/2badaaf8-7a5f-4142-a5b7-91aa698cc693)

## Analysis Procedures
### Check the present repurchase rate by SQL query
![olist_repurchase_rate_sql](https://github.com/Fan287/olist_analysis/assets/148685693/d5205689-619a-4471-8834-372bb4fd677d)
The result shows that the repurchase rate is approximately 3%, which is significantly low. To identify the reasons, customer comments are assumed to potentially provide some insights.

### Find out the customer's thought by Python (NLTK)
- NLTK is used to tokenize over 40,000 customers' comments and filter out the stop words. And it provides a list of frequency of meaningful words. The top ten of the list:
  -  ('product', 15871), ('delivery', 5316), ('arrived', 4937), ('time', 4845), ('good', 4452), ('recommend', 4422), ('received', 4403), ('delivered', 4268), ('deadline', 3075), ('came', 2824)
- Mainly, customers emphasized two things, the product quality and delivery. Since the dataset did not provide enough data for analysing product quality, this will not be the focus in this analysis. The focus will be studying the delivery, especially the shipping distance.

### Find out the shipping distance of orders by Python (Matplotlib, Pandas) and show the result in Power BI
- To draw the line between acceptable and far distance, matplotlib is used to demostrate at which distance level, the goods are needed to be delivered between two states.
![distance_categories_state](https://github.com/Fan287/olist_analysis/assets/148685693/47d2899d-56f8-4165-b970-e4025bedcbad)
  - Note: 0 and 1 represent 'order shipping across states' and 'order shipping within a state'
  - It shows most orders are shipped across states when the shipping distance is at 500 km. Thus, within 500 km will be treated as acceptable distance, more than 500 km as too far.
- To show the insight of distance, pandas' DataFrame of distance is imported to Power BI and The distance 
![order_distance](https://github.com/Fan287/olist_analysis/assets/148685693/abf6b6ac-1ce5-4824-ae86-7626815ff956)
  - Note: Orders with distances greater than or equal to 500 km are represented with blue color (light to dark shade); distances between 500 and 1000 km are represented with pink; distances between 1000 and 2000 km are represented with purple; distances over 2000 km are represented with red.
  - The graph shows that São Paulo State is a central point from which orders gradually expand outward, and transportation distance increases as orders move farther away from this province.
  - The orders with the farthest distances are concentrated in the coastal regions in the upper right corner.
  - This insight suggests that most sellers are located in São Paulo State, while other states have an undesirable sellers-to-customer ratio.

### To prove whether the insight is valid, find out the customers and sellers ratio in each state
![cust_sell_ratio](https://github.com/Fan287/olist_analysis/assets/148685693/53e120a6-912d-4f97-b22c-78aaf6c7a41d)
  - Note: The color of states is correspond to the graph of shipping distance. Blue is 1 seller: less than 100 customers; purple is between 100 to 200; red is between 200 to 4000.
  - The graph aligns with the graph of shipping distance. Blue areas are concentrated in the lower right corner, while other areas are either purple or red, indicating an unfavorable customers-to-sellers ratio.
  - In conclusion, the orders have long shipping distances because some states have too few sellers to meet local demand.  

## Recommendations to Olist
- The Recommendations: Encourage more sellers set up more warehouses and store specfic product categories in specific states 
  - recommendation of specfic product catgories in states with priority:
   ![product_recom_table](https://github.com/Fan287/olist_analysis/assets/148685693/e8867cb9-820a-43f6-bb59-5e0d6a930706)
    - The suggested ranking is based on a comparison of the sellers' ratios in each state. States with lower seller ratios are prioritized in the ranking.
    - As for the product recommendations, it involves calculating the difference between the number of items sold and purchased for each product category in each state. The top five product categories with the largest differences are then ranked in descending order
  - To persuade sellers, Olist can set up its own warehouses and sell the suggested products in these states for a period of six months. Olist should gather data during this period to demonstrate the profitability of such a business approach. Sellers would be more incentivized to join the plan when they see the potential for profit
  - The ideal outcome would be customers being able to buy products locally, thus reducing shipping time and costs. This may improve their user experience and encourage them to use Olist more frequently. As a result, the repurchase rate is expected to increase. 

