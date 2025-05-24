# Purpose
This data was created to try to answer the question "are video games getting worse?" There is a lot of talk about video games getting worse every year due to companies trying to maximize profits instead making quality games so I wanted to explore that idea.

Complete dataset with over 13,000 games on Kaggle. (https://www.kaggle.com/datasets/holmjason2/videogamedata/data)

# Content
This data file contains over 13,000 games which includes games ranging from 1977 to the middle of 2020. Most of the data came from directly from the VGChartz database but some has been manually entered in from other sources. For example a lot of the critic and user scores were entered from information available on Metacritic.

We initially imported the Video Game Sales dataset from Kaggle and cleaned the data by addressing missing values for critic_score and user_score.

# 1. Let's begin by looking at some of the top selling video games of all time!

```sql 
SELECT * FROM games_sales_data.game_sales_data
ORDER BY Total_Shipped DESC
LIMIT 10;
```
<img width="644" alt="{85E08B11-DED1-4F3B-95F8-539F3BA859B1}" src="https://github.com/user-attachments/assets/58874dcd-5094-4fc2-849a-7cf04b08d8b3" />



•  Nintendo games, particularly Wii Sports and the Super Mario series, demonstrate that strong sales and high user satisfaction can coexist, especially when developers maintain a focus on fun and accessibility.

•  The discrepancy between critic scores and user scores for games like PUBG and Minecraft shows that innovative ideas can lead to massive sales, but may also lead to mixed user reception, particularly if the game is unfinished or lacking polish in certain areas.



# 2. In which year where critic_score & user_score start dropping as games sales improve. 

```sql 
SELECT 
    Year, SUM(Total_Shipped) AS total_sales, 
    ROUND(AVG(User_Score), 2) AS avg_user_score, 
    ROUND(AVG(Critic_Score), 2) AS avg_critic_score
FROM games_sales_data.game_sales_data
GROUP BY Year
ORDER BY YEAR ASC;
```

| Year | Total Sales (in millions) | Avg User Score | Avg Critic Score |
|------|---------------------------|----------------|------------------|
| 1981 | 4.31                      | 7.8            | 7.6              |
| 1982 | 7.7                       | 7.4            | 9                |
| 1984 | 1.52                      | 7.4            | 9.5              |
| 1985 | 68.55                     | 8.25           | 8.75             |
| 1986 | 2.65                      | 8.1            | 8.5              |
| 1987 | 6.51                      | 8.8            | 8.4              |
| 1988 | 7.46                      | 8.1            | 8.5              |
| 1989 | 30.29                     | 5.45           | 8.2              |
| 1990 | 17.28                     | 9.3            | 9.8              |
| 1991 | 35.61                     | 8.8            | 8.55             |
| 1992 | 11.18                     | 8.5            | 9                |
| 1993 | 10.55                     | 9.5            | 9.2              |
| 1994 | 9.3                       | 8.8            | 9                |
| 1995 | 6.3                       | 8              | 8.9              |
| 1996 | 13.54                     | 8.5            | 8.87             |
| 1997 | 11.17                     | 9.25           | 9.45             |
| 1998 | 42.77                     | 8.8            | 9.05             |
| 1999 | 15.6                      | 9.1            | 8.38             |
| 2000 | 26.69                     | 8.45           | 8.2              |
| 2001 | 41.66                     | 7.77           | 8.94             |
| 2002 | 22.02                     | 8.85           | 9.2              |
| 2003 | 21.7                      | 9.04           | 8.58             |
| 2004 | 33.77                     | 7.91           | 8.64             |
| 2005 | 55.84                     | 7.62           | 7.83             |
| 2006 | 147.28                    | 8.26           | 8.11             |
| 2007 | 112.94                    | 8.57           | 8.32             |
| 2008 | 151.16                    | 8.55           | 8                |
| 2009 | 144.02                    | 8.57           | 7.77             |
| 2010 | 84.18                     | 8.78           | 8.3              |
| 2011 | 173.35                    | 6.59           | 7.06             |
| 2012 | 169.12                    | 7.06           | 7.37             |
| 2013 | 185.56                    | 6.98           | 7.55             |
| 2014 | 267.45                    | 7.01           | 7.5              |
| 2015 | 264.74                    | 6.89           | 7.42             |
| 2016 | 261.94                    | 6.92           | 7.41             |
| 2017 | 307.35                    | 6.81           | 7.39             |
| 2018 | 242.53                    | 6.58           | 7.33             |
| 2019 | 107.75                    | 6.45           | 7.86             |
| 2020 | 25.25                     | 7.5            | 8.74             |

 
From the result generated, average score for critic and user score ranging from 8 to 9 from year 1981 to 2010. 

•  A decrease in average score for both user and critic can be noticed from 2011 onward, particularly between 2011 (6.59) and 2013 (6.98), where it starts to hover between 6 and 7.

Starting from around year 2011 is whereby sales start to spike up from 173mil to year 2017 with 307.35mil of generated sales, suggesting that despite high sales, the quality perception (both from users and critics) might not have been as high.

•  By 2019 and 2020, the score is relatively low, with 6.45 in 2019 and 7.5 in 2020.
Potential analysis: The increase in sales in recent years might be due to greater accessibility or market expansion (e.g., digital distribution, wider audience reach), while the decline in user and critic scores might reflect issues with product quality, audience saturation, or other factors that affect perception.


# 3. Although 2017 generated the highest sales, our goal is to identify which publishers and games contributed most to these sales, along with their corresponding critic and user scores.

```sql 
SELECT Publisher,
    Name, 
    Year, 
    Total_Shipped, 
    ROUND(User_Score, 2) AS user_score, 
    ROUND(Critic_Score, 2) AS critic_score
FROM games_sales_data.game_sales_data
WHERE Year = 2017
ORDER BY Total_Shipped DESC
LIMIT 10;
```

<img width="543" alt="{BF590AAA-8896-487E-86F0-8B15630B9FFB}" src="https://github.com/user-attachments/assets/c17274f4-2513-42a9-b230-5e8fa676a063" />



•  Nintendo Dominated 2017: Their major titles like Zelda and Mario received perfect or near-perfect scores and performed strongly in sales.
•  PUBG's Popularity: Despite lower user ratings, PUBG became a phenomenon and had the highest sales, indicating that the battle royale genre was a major draw.



# 4.Top 10 games sales by Publisher

```sql 
SELECT Publisher, Year, SUM(Total_Shipped) AS total_sales, 
    ROUND(AVG(User_Score), 2) AS avg_user_score, 
    ROUND(AVG(Critic_Score), 2) AS avg_critic_score
FROM games_sales_data.game_sales_data
GROUP BY Publisher, Year
ORDER BY total_sales DESC
LIMIT 20;
```

## Video Game Sales Analysis by Publisher and Year

The table below shows the total sales, average user scores, and average critic scores for various publishers and games across different years.

| Publisher                           | Year | Total Sales (in millions) | Avg User Score | Avg Critic Score |
|-------------------------------------|------|---------------------------|----------------|------------------|
| Nintendo                            | 2006 | 120.96                    | 8.57           | 8.77             |
| Nintendo                            | 2017 | 83.76                     | 8.21           | 8.02             |
| Nintendo                            | 2009 | 72.28                     | 9.16           | 8.32             |
| Nintendo                            | 1985 | 68.55                     | 8.25           | 8.75             |
| Nintendo                            | 2013 | 68.23                     | 7.86           | 7.7              |
| Nintendo                            | 2018 | 61.76                     | 7.88           | 8                |
| Nintendo                            | 2011 | 56.37                     | 7.85           | 7.71             |
| Nintendo                            | 2008 | 55.03                     | 8.9            | 7.72             |
| Nintendo                            | 2019 | 49.94                     | 7.73           | 8.23             |
| Nintendo                            | 2014 | 48.98                     | 8.03           | 7.87             |
| Nintendo                            | 2005 | 48.79                     | 8.5            | 7.68             |
| Nintendo                            | 2007 | 43.26                     | 8.18           | 8.06             |
| Nintendo                            | 1998 | 42.63                     | 9.4            | 9.53             |
| Warner Bros. Interactive Entertainment | 2015 | 40.71                     | 7.13           | 7.99             |
| Valve                               | 2012 | 40                        | 7.5            | 8                |
| Nintendo                            | 2012 | 38.78                     | 7.38           | 7.38             |
| PUBG Corporation                    | 2017 | 36.6                      | 4.7            | 8.6              |
| Mojang                              | 2010 | 33.15                     | 7.8            | 10               |
| Electronic Arts                     | 2016 | 32.33                     | 6.45           | 8.39             |
| Activision                          | 2017 | 32.11                     | 5.02           | 8                |



Nintendo’s Consistency: Nintendo games are largely consistent in sales and in maintaining positive reception from both users and critics.

Strong Year for Nintendo in 2006: 2006 stands out as the peak of Nintendo's success with 120.96 million units sold, and solid user and critic ratings.’

Conclusion:

Sales don't always equal satisfaction: High sales figures do not guarantee positive user reception. Games like PUBG and some EA Sports titles show that success can be driven by external factors (genre trends, marketing, or timing), while users may not always be satisfied.

Nintendo's dominance is evident, but even they face challenges in maintaining consistent user satisfaction year over year.

1.	Sales Performance
Sales are increasing overall. This indicates that video games are reaching a wider audience, which in some cases can be seen as a positive trend (more people enjoying games).

The rise in sales doesn't necessarily mean the games are better or worse — commercial success can come from trends (like battle royales, nostalgia, or microtransactions).

2.	 Quality of Games (User vs. Critic Scores)
  User scores are dropping, particularly for franchise-heavy games and games with monetization strategies (microtransactions, DLCs, etc.).
 Critics are more generous, likely valuing technical or visual improvements, but users are increasingly dissatisfied, especially with annual releases that often don't innovate enough or seem designed to maximize profit.

Video games are not necessarily getting worse, but the gaming experience is changing. The commercial aspect is stronger than ever, but the creative freedom and player satisfaction may be diminishing in favor of profit-driven decisions.
This aligns with the idea that video games may feel worse to players because business models and industry practices are often compromising the quality of the games themselves.
