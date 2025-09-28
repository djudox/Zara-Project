USE [ZARA PROJECT]

SELECT * FROM [dbo].[zara]

--Check for Product_ID duplicates
--Before 252 rows
SELECT DISTINCT Product_ID FROM [dbo].[zara]
--After 252 rows - no duplicates

--Check for NULL Price values
SELECT Product_ID, Price FROM [dbo].[zara]
WHERE Price IS NULL
--No NULL Price values

--Creating a view to scrape some useless data and use it in Power BI
CREATE VIEW Zara_VW AS
SELECT Product_ID, Product_Position, Promotion, Product_Category, Seasonal, Sales_Volume, name, price, scraped_at, terms, section, SUM(Sales_Volume*Price) AS Total_Profit
FROM [dbo].[zara]
GROUP BY Product_ID, Product_Position, Promotion, Product_Category, Seasonal, Sales_Volume, name, price, scraped_at, terms, section

SELECT * FROM Zara_VW

SELECT Product_ID, Product_Position, Promotion, Product_Category, Seasonal, Sales_Volume, name, price, scraped_at, terms, section, SUM(Sales_Volume*Price) AS Total_Profit
FROM Zara_VW
WHERE Total_Profit > 50000
GROUP BY Product_ID, Product_Position, Promotion, Product_Category, Seasonal, Sales_Volume, name, price, scraped_at, terms, section
