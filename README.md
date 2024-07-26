# Amazon Prime Video Analysis

## Project Overview
This project involved analyzing Amazon Prime Video data using SQL and Power BI. The aim was to understand viewership trends, content performance, and customer preferences.

[GitHub repo](https://github.com/mahesh655/Amazon-Prime-Video-Analysis.git)

## Tools and Technologies
- **Database:** SQL
- **Visualization:** Power BI

## Key Insights and Features
- **Top Genres by Viewership:** This bar chart shows the genres with the highest viewership, helping to identify popular content categories. *Insight:* Drama and Comedy are the most-watched genres, while Documentary has the least viewership.
- **Monthly Active Users:** This line chart tracks the number of active users each month. *Insight:* There is a significant increase in user activity during the holiday season.
- **Content Performance by Region:** A heat map illustrating the performance of different content types across various regions. *Insight:* Action movies are highly popular in North America, while European viewers prefer Drama and Romance.
- **Average Watch Time by Age Group:** This pie chart shows the distribution of average watch time across different age groups. *Insight:* Younger audiences (18-25) spend the most time watching content, whereas older age groups have lower engagement.
- **Customer Ratings and Reviews Analysis:** A scatter plot displaying the relationship between customer ratings and the number of reviews. *Insight:* Higher-rated content tends to have more reviews, indicating higher engagement and satisfaction.
- **Interactive Filtering for Detailed Analysis:** An interactive dashboard allowing users to filter data based on genres, regions, and time periods. *Insight:* Enables detailed exploration of specific trends and patterns.

## Dashboard Images
[Link to Power BI report](https://app.powerbi.com/groups/me/reports/1a2b3c4d5e6f7g8h9i0j/ReportSection?experience=power-bi)

![Initial Dashboard](pics/amazon_prime1.png)
![Updated Dashboard](pics/amazon_prime2.png)

## SQL Queries Used

### Create User_Watch_History Table and Insert Data
```sql
CREATE TABLE User_Watch_History(
    UserId INT,
    WatchDate DATE,
    Genre TEXT,
    Region TEXT,
    WatchTime INT,
    AgeGroup TEXT,
    Rating FLOAT,
    Reviews INT
);

LOAD DATA INFILE 'D:/data/User_Watch_History.csv'
INTO TABLE User_Watch_History
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

### Top Genres by Viewership
```sql
SELECT Genre, SUM(WatchTime) AS TotalWatchTime
FROM User_Watch_History
GROUP BY Genre
ORDER BY TotalWatchTime DESC;

### Monthly Active Users
```sql
SELECT DATE_FORMAT(WatchDate, '%Y-%m') AS Month, COUNT(DISTINCT UserId) AS ActiveUsers
FROM User_Watch_History
GROUP BY Month
ORDER BY Month;

### Content Performance by Region
```sql
SELECT Region, Genre, SUM(WatchTime) AS TotalWatchTime
FROM User_Watch_History
GROUP BY Region, Genre
ORDER BY Region, TotalWatchTime DESC;

###Average Watch Time by Age Group
```sql
SELECT AgeGroup, AVG(WatchTime) AS AvgWatchTime
FROM User_Watch_History
GROUP BY AgeGroup
ORDER BY AvgWatchTime DESC;

### Customer Ratings and Reviews Analysis
```sql
SELECT Rating, COUNT(Reviews) AS ReviewCount
FROM User_Watch_History
GROUP BY Rating
ORDER BY Rating DESC;
### Interactive Filtering for Detailed Analysis
```sql
SELECT *
FROM User_Watch_History
WHERE Genre = 'Drama' AND Region = 'North America' AND WatchDate BETWEEN '2023-01-01' AND '2023-12-31';


