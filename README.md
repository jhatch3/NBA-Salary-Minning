# NBA-Salary-Minning


# Data Preprossing 

- NBA Advanced Data

1) Read data into drity csv based on season and team, see Data/dirty/ sub folders
2) Drop columns we wont use
3) Add teamname (short name ie BOS, POR)
4) Save data into Data/clean sub folder based on year and team
5) Add df to a master running data frame of every team for every year

- NBA Salary Data - ESPN stores all data in HTML So we can just loop through all years and pages. 

1) Build url f"https://www.espn.com/nba/salaries/_/year/{year}/page/{i}"
2) pd.read_html(url)[0]
3) Add year to data
4) Save master Salary df 

- Combine

1) use chatgpt to give me a key value pair that maps names from salary to names in nba advanced data frame, and Player-additional
3) create new columns for salary df and join based on Player-additional, Year
5) drop old naming convention
5) save as our final mastery data set

# Data Work Cited

RAW Advanced Data from https://www.basketball-reference.com/ 
Salary data https://www.espn.com/nba/salaries/_/


# Folder Tree

NBA-Salary/
├── main.ipynb
├── preprocessing.ipynb
├── df.png
│
└── Data/
├── nba_advanced_data.ipynb
├── nba_salaries.ipynb
├── team_colors.csv
├── names_advanced_tmp.csv
├── names_salaries_tmp.csv
│
├── dirty/
│ ├── 2020-21/
│ ├── 2021-22/
│ ├── 2022-23/
│ ├── 2023-24/
│ └── 2024-25/
│
└── clean/
├── nba_advanced_data.csv
├── nba_salaries_2021_to_2025.csv
├── master_data.csv
├── 2020-21/
├── 2021-22/
├── 2022-23/
├── 2023-24/
└── 2024-25/