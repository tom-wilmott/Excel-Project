# Premier League 24/25 Player Rating Dashboard

![Player Rating Dashboard](https://github.com/user-attachments/assets/4c75529e-9ba6-4c68-bc53-71c829c4095f)


## Introduction

This dashboard was created to help identify the best performing players in the 2024/25 Premier League season based on the users desired nationality, club and position. 

The data is from FBREF and Kaggle and provides an overview of player performances across the English Premier League during the 2024/25 season. The data was used to provide an overall score for each player based on their overall stats for the season.    

### Dashboard File
My final dashboard is in [Premier League 24-25 Player Rating Dashboard.xlsx](https://github.com/tom-wilmott/Excel-Project/blob/main/Premier%20League%2024-25%20Dashboard/Premier%20League%2024-25%20Player%20Rating%20Dashboard.xlsx).

### Excel Skills Used

The following Excel skills were utilized for analysis:

- **🔍 Power Query**
- **📉 Charts**
- **🧮 Formulas and Functions**
- **❎ Data Validation**

### Data Premier League Player Performance Dataset

The datasets used for this project contains total stats for the 562 players who played in the Premier League during the 2024/25 season. The datasets are available in (insert link to drive). They include detailed information on but not limited to:

- **⚽ Goals**
- **🅰️Assists**
- **🧤 Saves**
- **🧢 Appearances**

### 🔍 Power Query (ETL)

#### 📥 Extract

- I first used Power Query to extract the original FBFEF Data from (insert folder with all team data) where it was stored as 20 different files, one for each       Premier League team.

#### 🔄 Transform

- Then, I transformed the files into one query using the combine function before removing any unneccisary columns.

#### 🔗 Load

- Finally, I loaded the transformed query where I used it to complete any missing values in the Kaggle dataset and add a column for age.

  <img width="1688" height="794" alt="Screenshot 2025-09-17 102600" src="https://github.com/user-attachments/assets/80cbecf1-36af-4276-ad19-ec8ed29623db" />

### Scoring System

The key challenge of the scoring system was ensuring scores were compariable between players in different positions.
To address this I created 5 subscores that incorported different elements of football, which could then be used to create an overall score.

These were:

-  **🧤 Goalkeeper Score**
-  **🧱 Defending Score**
-  **🏃‍♂️ Involvement Score**
-  **⚽ Attacking Score**
-  **🧢 Apperance Score**

### 🧮 Formulas and Functions

#### Subscores

```
= player_stats[@[Clean Sheets]]/MAX('epl_player_stats_24_25 '!AI:AI)*0.5 +
  player_stats[@[Clearances]/MAX('epl_player_stats_24_25 '!AJ:AJ)*0.25 +
  player_stats[@[Tackles]/MAX('epl_player_stats_24_25 '!AM:AM)*0.25
```
- 🔢 Dividing by the Max value provides a percentage of how a player performs compared to the best player in each stat.
- ⚖️ The stats are weighted different to reflect their importance to the role and are combined to create the subscore.

Each subscore is created in a similar way but looks at different attributes.

#### Overall Score

```
=IFS(
E2="Goalkeeper",(7*F2 + 2*J2 + H2),
E2="Defender",(6*G2+3*H2+2*J2),
E2="Midfielder",(2*G2+3*H2+4*I2+3*J2),
E2="Forward",(6.25*I2+5*J2)
)
```
- 🔢 `IFS()` function ensures players are scored correctly based on their position.
- ⚖️ The subscores (columns F:J) are weighted differently to reflect their importance to each position and to ensure overall scores are comparible and accurate both within and across positions.

## Dashboard Build

### 📉 Charts

#### 📊 Best Player Score by Team - Bar Chart

<img width="509" height="286" alt="Screenshot 2025-09-17 091844" src="https://github.com/user-attachments/assets/5a583091-4750-4fcc-8b81-0ebb9bc3c4a7" />

- 🛠️ **Excel Features:** Utilized bar chart feature (with formatted score values) and optimized layout for clarity.
- 🎨 **Design Choice:** Horizontal bar chart for visual comparison of best scores.
- 📉 **Data Organization:** Sorted team by descending best score for improved readability.
- 💡 **Insights Gained:** This enables quick identification of teams with the best performing player, noting that Liverpool has the best scoring player when all players are considered.

#### 🗺️ Country Best Player Score - Map Chart

![Map Chart](https://github.com/user-attachments/assets/88ac0e0a-9860-425a-b058-a96c0420be46)

- 🛠️ **Excel Features:** Utilized Excel's map chart feature to plot best scores by each nationality.
- 🎨 **Design Choice:** Colour-coded map to visually differentiate scores across regions.
- 📊 **Data Representation:** Plotted best score for each country with available data.
- 👁️ **Visual Enhancement:** Improved readability and immediate understanding of geographic player performance trends.
- 💡 **Insights Gained:** Enables quick grasp of global player performance disparities in the Premier League and highlights high/low talent regions.

### 🧮 Formulas and Functions

####  Best Score by Team

```
=MAX(
  IF(
    (score[TEAM]=A2) *
    ((score[Nationality]=country) + (country="All")) *
    ((score[Position]=position) + (position="All")),
    score[Overall Score]
  )
)

```

- 🔍 **Multi-Criteria Filtering:** Checks team, nationality and position.
- 📊 **Array Formula:** Utilizes `MAX()` function with nested `IF()` statement to analyze an array.
- 🎯 **Tailored Insights:** Provides specific score information for players of different teams, nationalities, and positions.
- **🔢 Formula Purpose:** This formula populates the table below, returning the max score based on team, nationality, and position specified.

The above is very similar for the country and position charts.

🍽️ Background Table

<img width="373" height="506" alt="Screenshot 2025-09-17 092414" src="https://github.com/user-attachments/assets/daa31faa-15a9-4a04-8c28-19772afea455" />

#### 🧮 Formulas and Functions

```
=INDEX(
    SORTBY(
        A2:B22,
        INDEX(A2:B22,,2),
        -1
    ),
    SEQUENCE(5),
    {1,2}
)
```
- 📊 Using a combination of the `INDEX()`, `SORTBY()` and `SEQUENCE()` functions to manipulate the table to 5 values in the desired order to produce a refined table that is used for the chart.

<img width="285" height="143" alt="Screenshot 2025-09-17 092502" src="https://github.com/user-attachments/assets/18f6a683-cb6a-4cb3-85a3-913a1be2730e" />

##### 📉 Dashboard Implementation

<img width="504" height="397" alt="Screenshot 2025-09-17 093015" src="https://github.com/user-attachments/assets/7709cb47-edb2-4e18-94ec-c14ad55bed00" />


### 📢 Callout Values

#### 🥇 Best Player
```
=IF(high_score=0,"No Player Match",XLOOKUP(B2,'Score Table'!K:K,'Score Table'!A:A,FALSE))
```
#### 🎯 Score
```
=IFERROR(MAX(
IF(
  ((score[Club]=team) + (team="All"))*
  ((score[Nationality]=country) + (country="All"))*
  ((score[Position]=position) + (position="All")),
   score[Overall Score]
  )
),"N/A")
```
- **🔢 Formulas Purpose:** These formulas populate the table below, which provides the highest scoring player based on the active filters along with the score. Similar formulas are used to find the best under 23 player.

🍽️ Background Table

<img width="207" height="48" alt="Screenshot 2025-09-17 092744" src="https://github.com/user-attachments/assets/c96aa486-6c17-4e79-8c5e-96b7b161a68f" />

##### 📉 Dashboard Implementation:

<img width="518" height="567" alt="Screenshot 2025-09-17 092919" src="https://github.com/user-attachments/assets/dbc6f366-8ce2-4008-9dcb-15b8c94e3ed6" />

### ❎ Data Validation

#### 🔍 Filtered List

- 🔒 **Enhanced Data Validation:** Implementing the filtered list as a data validation rule under the `Team`, `Country`, and `Position` option in the Data tab ensures:
    - 🎯 User input is restricted to predefined, validated schedule types
    - 🚫 Incorrect or inconsistent entries are prevented
    - 👥 Overall usability of the dashboard is enhanced

![Data Validation](https://github.com/user-attachments/assets/e8638e23-8d76-4c57-bac9-a15ee480c767)

## Conclusion

I created this dashboard to showcase insights into the performance of players in the Premier League during the 2024/25. Utilizing data available to me, this dashboard allows users to explore the best players for their desired criteria and in theory could be utilized for scouting purposes. Exploring the functionalities to understand how players of different teams, nationalites and position performed. 
