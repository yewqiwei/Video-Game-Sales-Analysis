# Purpose
This data was created to try to answer the question "are video games getting worse?" There is a lot of talk about video games getting worse every year due to companies trying to maximize profits instead making quality games so I wanted to explore that idea.

# Content
This data file contains over 13,000 games which includes games ranging from 1977 to the middle of 2020. Most of the data came from directly from the VGChartz database but some has been manually entered in from other sources. For example a lot of the critic and user scores were entered from information available on Metacritic.

We initially imported the Video Game Sales dataset from Kaggle and cleaned the data by addressing missing values for critic_score and user_score.

# 1. Let's begin by looking at some of the top selling video games of all time!

SELECT * FROM games_sales_data.game_sales_data
ORDER BY Total_Shipped DESC
LIMIT 10;

![image](https://github.com/user-attachments/assets/3d2ae1a4-d285-4839-aae2-7508f41c6cfa)


•  Nintendo games, particularly Wii Sports and the Super Mario series, demonstrate that strong sales and high user satisfaction can coexist, especially when developers maintain a focus on fun and accessibility.
•  The discrepancy between critic scores and user scores for games like PUBG and Minecraft shows that innovative ideas can lead to massive sales, but may also lead to mixed user reception, particularly if the game is unfinished or lacking polish in certain areas.



# 2. In which year where critic_score & user_score start dropping as games sales improve. 

SELECT 
    Year, SUM(Total_Shipped) AS total_sales, 
    ROUND(AVG(User_Score), 2) AS avg_user_score, 
    ROUND(AVG(Critic_Score), 2) AS avg_critic_score
FROM games_sales_data.game_sales_data
GROUP BY Year
ORDER BY YEAR ASC;

![image](https://github.com/user-attachments/assets/dd0bb96a-b0a2-421f-a03b-fbbe5551d07b)

 
From the result generated, average score for critic and user score ranging from 8 to 9 from year 1981 to 2010. 

•  A decrease in average score for both user and critic can be noticed from 2011 onward, particularly between 2011 (6.59) and 2013 (6.98), where it starts to hover between 6 and 7.

Starting from around year 2011 is whereby sales start to spike up from 173mil to year 2017 with 307.35mil of generated sales, suggesting that despite high sales, the quality perception (both from users and critics) might not have been as high.
•  By 2019 and 2020, the score is relatively low, with 6.45 in 2019 and 7.5 in 2020.
Potential analysis: The increase in sales in recent years might be due to greater accessibility or market expansion (e.g., digital distribution, wider audience reach), while the decline in user and critic scores might reflect issues with product quality, audience saturation, or other factors that affect perception.


# 3. Despite year 2017 generated the higher sales, we would like to identify which publishers and games contributed to the highest sales, along with the critic_scores and user_score

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


![image](https://github.com/user-attachments/assets/4c9bcd64-e56b-4ec2-8d65-dcc0dc5a752a)

 

•  Nintendo Dominated 2017: Their major titles like Zelda and Mario received perfect or near-perfect scores and performed strongly in sales.
•  PUBG's Popularity: Despite lower user ratings, PUBG became a phenomenon and had the highest sales, indicating that the battle royale genre was a major draw.



# 4.Top 10 games sales by Publisher

SELECT Publisher, Year, SUM(Total_Shipped) AS total_sales, 
    ROUND(AVG(User_Score), 2) AS avg_user_score, 
    ROUND(AVG(Critic_Score), 2) AS avg_critic_score
FROM games_sales_data.game_sales_data
GROUP BY Publisher, Year
ORDER BY total_sales DESC
LIMIT 20;

![image](https://github.com/user-attachments/assets/6b6e9615-c308-4d97-9704-b7459b4bbba1)



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
