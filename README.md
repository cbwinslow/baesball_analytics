# Baseball Analytics
## Overview

The free and open-source baseball data sets from Lahman and Retrosheet will be downloaded, wrangled, and analyzed.

## Sabermetrics

Sabermetrics is a term coined prior to the advent of modern software tools for data analysis with fast personal computers.  One aim is to create metrics that make it easy for people to quickly grasp how much a player contributes to his team's wins.

With Pandas and Scikit Learn, comprehensive models can now easily be created, but this does not diminish the value of Sabermetrics.  Most of the thinking behind Sabermetrics is relevant to all data analysis.  Both modern data analysis and Sabermetrics will be presented in Jupyter Notebooks.

### Data Preparation

The Python scripts prepare the data for analysis.  This includes running the open-source Retrosheet parsers.  See:   These scripts are located in this repo at: [download_scripts](https://github.com/sdiehl28/baseball-analytics/tree/master/download_scripts).

A script is also provided to load the wrangled data into Postgres with primary and foreign key constraints.  Use of Postgres is optional.

### Data Analysis

Examples of interesting baseball questions are answered using Jupyter Notebooks with Python, Pandas and matplotlib/seaborn plots.

Some questions include:

* How many more runs per game are there when the DH is used?  Could this difference be due to chance?
* How has game length and pitcher count increased over the years?
* How is game length related to pitcher count?  Could this relationship be due to chance?

These Jupyter Notebooks are in this repo at: [Baseball Analysis](https://github.com/sdiehl28/baseball-analytics/tree/master/baseball_jupyter_nb).

### Data Validation

pytest is used to automate data integrity and data consistency testing.  More than 100 attributes are checked over the last 45 years worth of data.  Some examples:

* the number of home runs hit by batters should equal the number of home runs allowed by pitchers
* when the Retrosheet data aggregated to the same level as Lahman data, the two data sets should be consistent with each other
* fields which should uniquely identify a row in a CSV file, actually do.

### Ongoing

Additional examples of baseball data analysis are continually being added.

Retrosheet postseason data will soon be parsed.  All Retrosheet regular season data has been parsed and wrangled for use.

## MLB Data Wrangling

There are two primary sources of free and extensive baseball data:

* Lahman
* Retrosheet

The Lahman data is tidy and is therefore easy to use with Pandas or SQL, however the data is per season rather than per game.  Finding a team's win streaks, a player's best month for hitting, and similar is not possible with the Lahman data.

The Retrosheet data is play-by-play data which is arguably too fine grained and must be parsed and summarized to the game level.  To make it easy to use, it must be made tidy.

Having both data sets available allows for queries such as what was the longest hitting streak for all players who earned in the top 10% of salary that year.

The scripts in this repo will wrangle the Lahman and Retrosheet data to create csv files to:

* allow for easy Pandas analysis (or SQL analysis if loaded into a database)
* allow both data sets to be referenced in the same query
* ensure that for both data sets, the same 50+ field names are used to represent the same information
  * for example, if a batter hits a "hr", then the opposing pitcher gave up a "hr" and "hr" is the field name used in the batting and pitching csv files for both Lahman and Retrosheet
* ensure that field names conform to official baseball abbreviations as much as possible
* ensure that all field names are valid Python identifiers and valid SQL column names
* determine the most efficient data type, for both Pandas and SQL, and persist that data type for each field in a corresponding csv file
  * code is provided to read/write csv files with persisted data types
* parse the Retrosheet data using open-source parsers (which on Linux must be built from source code)
* tidy the Retrosheet data, identify primary keys and sum stats for the exceptionally few players who had multiple records with the same primary key
* ensure that the data is accurate by providing more than 50 pytest tests to verify that the restructured data is consistent between the two data sets, the Retrosheet data produced by the parsers is completely consistent between parsers, the primary keys are unique, etc.  

At this time, the restructured data is not provided in this repo, only the scripts to create it are provided.

If you have any questions, you may send me an email with the word "baseball" in the subject to: sdiehl28@gmail.com

## Development Environment

The scripts and Jupyter Notebooks were testing using Python 3.7 in a full [Anaconda](https://www.anaconda.com/distribution/) 2019.10 environment.  Note that the [open-source parsers](https://sourceforge.net/projects/chadwick/) for Retrosheet must be installed to run the scripts.  See:  [Retrosheet Parsers](https://github.com/sdiehl28/baseball-analytics/blob/master/RetrosheetParsers.md).

## Additional Information

For more information about the Lahman and Retrosheet data sets and how they were wrangled, see: [MLB Data Overview](https://github.com/sdiehl28/baseball-analytics/blob/master/MLB_Data_Overview.md)

For even more information, such as the Lahman and Retrosheet data licenses and the Retrosheet parsers, see: [MLB Data Details](https://github.com/sdiehl28/baseball-analytics/blob/master/MLB_Data_Details.md)




