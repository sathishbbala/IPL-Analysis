# IPL-Analysis
A Power BI Dashboard that provides comprehensive insights into Indian Premier League (IPL) data, tracking team performances, batsman statistics, and bowler metrics across multiple seasons.
## 🚀 Live Link & Preview

<img width="1433" height="807" alt="image" src="https://github.com/user-attachments/assets/ec314a14-982b-4686-8d35-1092fade22c7" />

## 📊 Key Features & Insights

* Match Performance: High-level overview of match wins, tosses, and venue statistics.
* Batsman Analysis: Detailed breakdown of top run-scorers, strike rates, boundaries (4s/6s), and averages.
* Bowler Analysis: Evaluation of leading wicket-takers, economy rates, bowling averages, and dot-ball percentages.
* Team Standings: Historical trends of how teams performed across different IPL seasons.

## 🛠️ Tech Stack & Tools

* Business Intelligence: Power BI Desktop
* Data Transformation: Power Query (ETL process, data cleaning, and handling missing values)
* Calculations: DAX (Data Analysis Expressions) for dynamic measures and KPIs
* Data Source: [Mention source, e.g., Kaggle / Cricsheet] CSV/Excel dataset

## 📐 Data Model & DAX Measures
This project utilizes a Star Schema data model, connecting a central Fact table (ball by ball) with multiple Dimension tables (Teams, Players, Matches).
Some of the key DAX measures created for this dashboard include:
''' dax
NumberOfCenturies = 
VAR SelectedSeason = SELECTEDVALUE(ipl_matches_data[season])
VAR SeasonData = FILTER(ball_by_ball_data, RELATED(ipl_matches_data[season]) = SelectedSeason)
VAR BatterRuns = 
    ADDCOLUMNS(
        SUMMARIZE(
            SeasonData, 
            ball_by_ball_data[match_id], 
            ball_by_ball_data[batter]
        ),
        "TotalRuns", CALCULATE(SUM(ball_by_ball_data[batter_runs]))
    )
-- Step 2: Filter that table for scores >= 100 and count the rows
VAR CountOfCenturies = 
    COUNTROWS(
        FILTER(
            BatterRuns,
            [TotalRuns] >= 100
        )
    )
RETURN
    -- Step 3: Return the count (or 0 if they haven't scored a century)
    IF(ISBLANK(CountOfCenturies), 0, CountOfCenturies)
'''
## ⚙️ How to Run This Project Locally

   1. Clone this repository to your local machine.
   2. Download and install Power BI Desktop (if you haven't already).
   3. Open the .pbix file included in this repository.
   4. (Optional) If the data paths break, redirect the data source settings to the CSV files inside the /Data folder.

