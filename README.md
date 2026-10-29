**#Experiment 1: EDA in IPL Dataset**
**Aim:**
To perform Exploratory Data Analysis (EDA) on the IPL matches dataset and derive insights about matches per season, winning teams, toss decisions, and top venues.

**Algorithm / Procedure:**

**1.Import Libraries**
  Import pandas for data handling.
  Import matplotlib and seaborn for visualization.
  
**2.Load Dataset**
  Use pd.read_csv() to load the IPL matches dataset.
  Check dataset shape using .shape.
  View first 5 rows using .head().
  
**3.Matches per Season (Univariate Analysis)**
  Group data by season and count matches.
  Plot a bar chart to visualize growth/decline in matches.
  
**4.Top Winning Teams (Univariate Analysis)**
  Use value_counts() on the winner column.
  Plot top 5 winning teams in a bar chart.
  
**5.Toss Decisions (Univariate Analysis)**
  Count toss decision preferences (bat vs field).
  Plot results using a bar chart.
  
**6.Top Venues (Univariate Analysis)**
  Count matches per venue.
  Display top 5 venues with a horizontal bar chart.
  
**7.Draw Insights**
  Observe patterns in toss decisions.
  Identify teams with consistent winning trends.
  
  **Program**
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
df=pd.read_csv("matches.csv")
print("Rows:",df.shape[0])
print("Columns:",df.shape[1])
print(df.head())
print(df.dtypes)
print("Unique id: ",df["id"].nunique())
print("Is ID Unique: ",df["id"].is_unique)
print(df.isnull().sum()[df.isnull().sum()>0])
print(df.duplicated().sum())
df["city"]=df["city"].fillna("Unknown")
season_matches=df.groupby("season").size()
print(season_matches)
print("Season with most matches:",season_matches.idxmax())
print("Highest number of matches:",season_matches.max())
winners=(
df.dropna(subset=["winner"]).groupby("winner").size().sort_values(ascending=False))
print(winners.head(5))
csk=df[df["winner"]=="Chennai Super Kings"]
print(csk[["season", "team1", "team2", "winner"]].head(10))
print("Total matches won by CSK: ",len(csk))
toss_count=df["toss_decision"].value_counts()
toss_percent=df["toss_decision"].value_counts(normalize=True)*100
print("Frequency")
print(toss_count)
print("Percentage")
print(toss_percent.round(2))
print("Most preferred decision: ",toss_count.idxmax())
toss_season=pd.crosstab(df["season"],df["toss_decision"])
print(toss_season)
print("\nMost preferred decision by season: ")
print(toss_season.idxmax(axis=1))
venues = df.groupby("venue").size().sort_values(ascending=False)
print(venues.head(5))
margin_df = df.dropna(subset=["result_margin"])
largest = margin_df.loc[margin_df["result_margin"].idxmax()]
print("Largest winning margin:", largest["result_margin"])
print(largest[[
    "season", "team1", "team2", "winner",
    "result", "result_margin"
]])

print("\nTop 10 winning margins:")
print(
    margin_df.sort_values("result_margin", ascending=False)
    [["season", "team1", "team2", "winner", "result_margin"]]
    .head(10).to_string(index=False)
)
print("\nQ12. MATCH RESULT ANALYSIS")
print(df["result"].value_counts())
print("Before conversion:", df["date"].dtype)
df["date"] = pd.to_datetime(df["date"], errors="coerce")
print("After conversion:", df["date"].dtype)
df["year"] = df["date"].dt.year
print(df[["date", "year"]].head(10).to_string(index=False))
win_type_map = {
    "runs": "Won by Runs",
    "wickets": "Won by Wickets",
    "tie": "Tie",
    "no result": "No Result"
}
df["win_type"] = df["result"].map(win_type_map).fillna("Other")
print(df[["result", "win_type"]].head(10).to_string(index=False))
player=df.groupby("player_of_match").size().sort_values(ascending=False)
print(player.head(10))
```

  **Output**

  <img width="752" height="706" alt="image" src="https://github.com/user-attachments/assets/67a77594-40ec-4f5e-b4f2-b1ef492f05e4" />
  <img width="347" height="420" alt="image" src="https://github.com/user-attachments/assets/80590c0c-5591-4d19-93a7-eb330b63501f" />
  <img width="221" height="62" alt="image" src="https://github.com/user-attachments/assets/09156c5c-4946-4ea4-b931-1217de66dac9" />
  <img width="292" height="193" alt="image" src="https://github.com/user-attachments/assets/92c924cd-df9c-409c-9936-9ffd29a41a05" />
  <img width="465" height="418" alt="image" src="https://github.com/user-attachments/assets/d354e2cb-37fb-4773-a482-c71dc90c02ea" />
  <img width="406" height="150" alt="image" src="https://github.com/user-attachments/assets/52a8d473-8547-40be-a11e-5c4bd08b3bc9" />
  <img width="732" height="462" alt="image" src="https://github.com/user-attachments/assets/76d72a1c-804e-40c0-96b4-6573be645027" />
  <img width="456" height="193" alt="image" src="https://github.com/user-attachments/assets/cb015bdb-5b53-41fd-8fa8-6aa4b2bc2857" />
  <img width="553" height="777" alt="image" src="https://github.com/user-attachments/assets/580adfc1-836d-4b79-ada3-31b691188e1f" />
  <img width="470" height="152" alt="image" src="https://github.com/user-attachments/assets/23900fc9-f9bf-4034-8567-3145680f662c" />
  <img width="985" height="423" alt="image" src="https://github.com/user-attachments/assets/f6178bab-bcc6-4ad5-b912-7b4e02317588" />
  <img width="362" height="142" alt="image" src="https://github.com/user-attachments/assets/2d773a2f-a0c7-4fd5-bf2b-1898ed706a8b" />
  <img width="312" height="56" alt="image" src="https://github.com/user-attachments/assets/f0559334-5fa6-4d61-9d4a-592a0a27ddb0" />
  <img width="283" height="227" alt="image" src="https://github.com/user-attachments/assets/fbbd3354-1d82-40bf-be14-91450b31f359" />
  <img width="295" height="227" alt="image" src="https://github.com/user-attachments/assets/88d06f5b-f49e-4292-97bd-1199dbc53965" />
  <img width="288" height="242" alt="image" src="https://github.com/user-attachments/assets/08425caa-0021-4f35-9c66-455f54df79c9" />


 **Result**
 
  This experiment is executed successfully



Highlight the stadiums hosting maximum matches.
