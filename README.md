# ecommerce_sales_analysis
Questions Answered :

Q.1 💰 What is the total revenue generated overall?

SELECT SUM(revenue) AS total_revenue_generated
FROM ecommerce_data;

Q.2 🛍️ Which are the top 5 products by total revenue?

SELECT product_name, SUM(revenue) AS total_revenue
FROM ecommerce_data
GROUP BY product_name
ORDER BY total_revenue DESC
LIMIT 5;

Q.3 📦 Which category has the highest number of units sold?

SELECT category, SUM(units_sold) AS units_sold
FROM ecommerce_data
GROUP BY category
ORDER BY units_sold DESC
LIMIT 1;

Q.4  🏪 Which seller generated the highest and lowest revenue?

SELECT seller_name, SUM(revenue) AS total_revenue
FROM ecommerce_data
GROUP BY seller_name
ORDER BY total_revenue DESC;

Q.5  🔁 Which products have the highest return rate?

SELECT product_name, return_rate
FROM ecommerce_data
ORDER BY return_rate DESC
LIMIT 10;

Q.6  ⭐ Which products have low ratings (<3.0) and high return rate (>15%)?

SELECT product_name, rating, return_rate
FROM ecommerce_data
WHERE rating < 3.0 AND return_rate > 0.15;

Q.7 📊 What is the average rating and return rate by category?

SELECT category,
       ROUND(AVG(rating),2) AS average_rating,
	   ROUND(AVG(return_rate),2) AS average_return_rate
FROM ecommerce_data
GROUP BY category;

Q.8 📉 Which seller has the highest average return rate?

SELECT seller_name, ROUND(AVG(return_rate),2) AS highest_return_rate
FROM ecommerce_data
GROUP BY seller_name
ORDER BY highest_return_rate DESC
LIMIT 1;

Q.9 💡 Is there a correlation between product rating and return rate?

SELECT rating, return_rate
FROM ecommerce_data;

Q.10 ⚠️ Which products should be flagged for review due to low sales, low rating, and high return?

SELECT product_name, units_sold, rating, return_rate
FROM ecommerce_data
WHERE units_sold < 80 AND rating < 2 AND return_rate > 0.10;

Q.11 🥈 Which seller has the 2nd highest total revenue?

SELECT seller_name, SUM(revenue) AS total_revenue
FROM ecommerce_data
GROUP BY seller_name
ORDER BY total_revenue DESC
OFFSET 1
LIMIT 1;

Q.12 💸 Which products are overpriced (high price but low rating)?

SELECT product_name,price, rating
FROM ecommerce_data
WHERE price > (SELECT AVG(price) FROM ecommerce_data) 
	AND rating < 2.5
ORDER BY price DESC
LIMIT 5;





