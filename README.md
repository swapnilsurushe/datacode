# datacode


Certainly, here are example README files for Question 1 and Question 2 code submissions. You should customize these README files to include specific details related to your code and project.

**README for Question 1 - Data Ingest Process:**

# Data Ingest Process for ODI Cricket Match Data

This repository contains the code and documentation for the data ingest process as part of the Data Engineering Assessment.

## Overview

The objective of this project is to develop a batch data ingest process to load One Day International (ODI) cricket match results and ball-by-ball innings data. The data is sourced from cricsheet.org and is provided in JSON format. This code demonstrates how to download the data, preprocess it, and store it in a SQLite database.

## Requirements

- Python 3.8
- PySpark
- SQLite
- Dependencies listed in `requirements.txt`

## Usage

1. Clone this repository to your local machine.

```bash
git clone [repository_url]
cd data-ingest-process
```

2. Install the required Python packages.

```bash
pip install -r requirements.txt
```

3. Run the data ingest process by executing the Python script.

```bash
python data_ingest.py
```

4. Follow the prompts in the command line to download, preprocess, and store the data.

## Database Schema

The SQLite database schema includes the following tables:

- `matches`: Contains match results.
- `innings`: Contains ball-by-ball innings data.
- `players`: Contains player information.

## Sample Data

A sample dataset is provided for testing purposes in the `sample_data` directory.

## Acknowledgments

- Data sourced from cricsheet.org
- The project was completed as part of a data engineering assessment.

**README for Question 2 - SQL Queries:**

# SQL Queries for ODI Cricket Match Data Analysis

This repository contains SQL queries to analyze One Day International (ODI) cricket match data stored in the SQLite database.

## Overview

The SQL queries in this project are designed to answer specific questions about ODI cricket match data, including win records, the highest win percentages in 2019, and the players with the highest strike rates in 2019.

## Usage

1. Ensure that the SQLite database, populated with ODI cricket match data, is set up.

2. Execute the SQL queries provided in the SQL files to obtain the desired insights.

3. The SQL files include:
   - `query_a.sql`: Win records (percentage win and total wins) for each team by year and gender, excluding ties, matches with no result, and matches decided by the DLS method.
   - `query_b.sql`: Male and female teams with the highest win percentages in 2019.
   - `query_c.sql`: Players with the highest strike rate as batsmen in 2019, accounting for handling extras properly.

## Example Queries

Below are example queries to provide a glimpse of the analysis:

### Query A - Win Records by Year and Gender

```sql
-- Sample SQL query to retrieve win records by year and gender, excluding specific results.
SELECT
    year,
    gender,
    team,
    SUM(CASE WHEN result = 'win' THEN 1 ELSE 0 END) AS total_wins,
    100 * SUM(CASE WHEN result = 'win' THEN 1 ELSE 0 END) / COUNT(*) AS win_percentage
FROM matches
WHERE result NOT IN ('tie', 'no result', 'DLS')
GROUP BY year, gender, team;
```

### Query B - Highest Win Percentages in 2019

```sql
-- Sample SQL query to identify male and female teams with the highest win percentages in 2019.
SELECT
    gender,
    team,
    MAX(win_percentage) AS max_win_percentage
FROM (
    SELECT
        gender,
        team,
        SUM(CASE WHEN result = 'win' THEN 1 ELSE 0 END) AS total_wins,
        100 * SUM(CASE WHEN result = 'win' THEN 1 ELSE 0 END) / COUNT(*) AS win_percentage
    FROM matches
    WHERE year = 2019 AND result NOT IN ('tie', 'no result', 'DLS')
    GROUP BY gender, team
) subquery;
```

## Acknowledgments

- The project was completed as part of a data engineering assessment.
- The sample data was sourced from cricsheet.org.

Please note that the specific details in these README files should correspond to your actual code and project.
