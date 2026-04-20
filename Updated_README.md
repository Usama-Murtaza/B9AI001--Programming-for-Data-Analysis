# Anime Metadata, Genre, and Popularity Trend Analysis Pipeline

## Project Summary

This project builds a complete data acquisition and preprocessing pipeline for anime metadata using a public API. The notebook collects anime data from the Jikan REST API, converts the raw JSON into a tabular format, cleans and transforms the data, stores both raw and processed records in a SQLite database, runs queries and visual analysis, and includes testing and a simple search interface.

The main notebook file for this project is `Anime_updated.ipynb`.

This README is a full project README and authorship audit. It focuses only on what is present in the notebook and what can reasonably be inferred from the notebook structure, comments, and coding style.

## What the Notebook Does

The notebook is organised as a pipeline with these stages:

1. installs the required libraries
2. imports Python packages
3. sets configuration values such as the API base URL, database name, search query, number of pages, and request delay
4. defines helper functions for cleaning text, converting numeric values safely, classifying score and popularity ranges, grouping anime by episode count, and extracting names from nested lists
5. fetches anime data from the Jikan API using either a search query or the top anime endpoint
6. normalises the raw JSON response into a pandas DataFrame
7. preprocesses the data and creates new features
8. creates a SQLite database with `raw_anime` and `processed_anime` tables
9. inserts raw and processed data into the database
10. runs database queries for analysis
11. runs unit tests
12. runs an integration test for the full pipeline

## Data Source

This project uses the Jikan REST API v4 as the source of anime metadata. In the notebook, the API base URL is set as:

```python
BASE_URL = "https://api.jikan.moe/v4"
```

The notebook uses the search endpoint and also supports the top anime endpoint through the `fetch_anime_search()` and `fetch_top_anime()` functions.

## Main Functions and Sections in the Notebook

### Configuration
The notebook defines:
- `BASE_URL`
- `DB_NAME`
- `SEARCH_QUERY`
- `MAX_PAGES`
- `REQUEST_DELAY`

These values control the source of the data, the query used, the number of pages fetched, and the delay between requests.

### Helper Functions
The notebook contains helper functions such as:
- `clean_text()`
- `safe_int()`
- `safe_float()`
- `classify_score_band()`
- `classify_popularity_band()`
- `classify_episode_group()`
- `extract_names_from_list()`
- `count_items_in_csv()`

These support text cleaning, safe type conversion, category creation, extraction from nested JSON, and counting logic.

### Data Acquisition
The notebook uses:
- `fetch_anime_search()`
- `fetch_top_anime()`

These functions request paginated anime data from the Jikan API.

### Data Normalisation
The notebook uses:
- `normalize_anime_data()`

This function converts raw JSON data into a structured pandas DataFrame and extracts fields such as title, English title, type, source, episodes, status, score, popularity, synopsis, genres, themes, studios, demographics, year, season, URL, and fetch time.

### Preprocessing and Feature Engineering
The notebook uses:
- `preprocess_anime_data()`

This function:
- removes duplicate anime using `mal_id`
- cleans title and synopsis fields
- converts numeric columns safely
- creates new features such as:
  - `clean_title`
  - `clean_title_english`
  - `clean_synopsis`
  - `title_length`
  - `synopsis_length`
  - `has_english_title`
  - `score_band`
  - `popularity_band`
  - `episode_group`
  - `genre_count`
  - `theme_count`
  - `studio_count`
  - `demographic_count`

### Database Creation and Insertion
The notebook uses:
- `create_database()`
- `insert_raw_anime()`
- `insert_processed_anime()`

The database includes two tables:
- `raw_anime`
- `processed_anime`

This keeps original API data separate from transformed data.

### Query and Analysis Functions
The notebook defines functions such as:
- `get_all_processed_anime()`
- `search_anime_by_title()`
- `get_average_score_by_type()`
- `get_anime_count_by_year()`
- `get_top_genres()`
- `get_top_studios()`
- `get_score_band_summary()`
- `get_popularity_band_summary()`

These functions retrieve and summarise stored data for analysis.


### Testing
The notebook includes:
- a `TestAnimePipelineFunctions` unit test class
- an `integration_test_pipeline()` function

The unit tests check important helper and transformation functions. The integration test checks the full flow from API fetch to database retrieval.

### Frontend and Backend Interaction
The notebook uses:
- `gradio_search()`
- `gr.Interface(...)`

This creates a simple interface that lets a user enter an anime title and retrieve matching results from the SQLite database.

## External Sources and Libraries Used

This section lists the external sources, tools, libraries, and public services used in the notebook.

### 1. Jikan REST API
The anime data comes from the Jikan REST API.

Used for:
- anime data acquisition
- paginated API requests
- search based anime retrieval
- top anime retrieval

### 2. Python Libraries
The notebook imports and uses:
- `requests`
- `sqlite3`
- `pandas`
- `re`
- `string`
- `time`
- `collections.Counter`
- `datetime`
- `matplotlib.pyplot`
- `unittest`
- `gradio`

Used for:
- API requests
- database creation and querying
- data manipulation
- text cleaning
- request delay handling
- counting
- time and date handling
- plotting
- testing
- interface creation

### 3. Standard Programming Patterns
The notebook also uses standard Python and SQL patterns such as:
- looping through paginated API responses
- converting JSON into row dictionaries
- building a pandas DataFrame from a list of rows
- using `INSERT OR IGNORE` in SQLite
- using `unittest.TestCase`
- returning top counts with `Counter`
- building a basic `gr.Interface`

These patterns are common practice and are not unique to one source.

## Full AI and Authorship Audit

This section is a stricter audit of the notebook. It is based on:
- explicit comments already inside the notebook
- the structure and style of the code
- the style and tone of markdown cells
- the level of polish and consistency across sections

This section does not claim certainty where certainty is not possible. It identifies what should reasonably be declared as AI generated or AI assisted based on the notebook itself.

## Parts Clearly Marked in the Notebook as AI Written

The notebook itself directly indicates the following parts were AI written or AI assisted:

1. `normalize_anime_data()`
   - notebook comment says the logic was self devised and the code was AI written for efficiency

2. `preprocess_anime_data()`
   - notebook comment says the logic was self devised and the code was AI written for efficiency

3. `run_pipeline()`
   - notebook comment says the code was AI written for efficiency

4. `TestAnimePipelineFunctions`
   - notebook comment says this test class was written by AI


### 1. Most markdown or documentation cells

This likely includes:
- introduction and project summary
- pipeline explanation
- data acquisition explanation
- raw data normalisation explanation
- preprocessing explanation
- transformed features explanation
- database design explanation
- query and analysis explanation
- testing explanation
- ethical considerations explanation
- conclusion style markdown cells

### 2. Many function docstrings

This likely applies to:
- `clean_text()`
- `safe_int()`
- `safe_float()`
- `classify_score_band()`
- `classify_popularity_band()`
- `classify_episode_group()`
- `extract_names_from_list()`
- `count_items_in_csv()`
- API functions
- query functions
- plotting functions
- testing functions


### 3. Overall notebook scaffold
The notebook follows a very clean pipeline template:
- install packages
- imports
- configuration
- helper functions
- acquisition
- normalisation
- preprocessing
- database creation
- database insertion
- queries
- plots
- tests
- interface

This structure is sensible and strong, but it also strongly suggests AI assistance in project scaffolding or notebook organisation.

### 4. Query helper functions
The cluster of compact analysis functions appears highly consistent in style and naming.

This likely includes:
- `get_all_processed_anime()`
- `search_anime_by_title()`
- `get_average_score_by_type()`
- `get_anime_count_by_year()`
- `get_top_genres()`
- `get_top_studios()`
- `get_score_band_summary()`
- `get_popularity_band_summary()`


### 6. Gradio interface section
The frontend block looks is a AI suggested extension for demonstrating frontend and backend interaction.

This likely includes:
- `gradio_search()`
- `gr.Interface(...)`


### 7. Integration test structure
Even though only the unit test class is explicitly marked as AI written, the integration test follows a very standard AI style workflow:
- fetch
- normalise
- preprocess
- create test database
- insert data
- retrieve data
- assert success

## Parts Claimed as Own Work

- choosing the anime topic
- choosing the Jikan API as the source
- choosing SQLite as the database
- deciding to use `raw_anime` and `processed_anime`
- deciding what fields to extract from the API response
- choosing features such as `score_band`, `popularity_band`, and `episode_group`
- choosing configuration values such as search query, page limit, and request delay
- running the notebook in Colab
- testing the notebook
- debugging issues such as missing variables, duplicate insertions, and integration test failures
- deciding how the project should match the assessment brief
- reviewing, editing, and presenting the final notebook
- tracking whole progress at github.

A fair description of this notebook is:

> The project topic, data source choice, feature choices, database direction, execution, debugging, and final review were done by the student. AI was used to help draft parts of the code, notebook structure, markdown documentation, tests, helper functions, query functions, visualisation helpers, and interface code. All final code was reviewed, run, and integrated into the final working notebook by the student.

## Suggested Authorship Breakdown Table

| Notebook Part | Likely Origin | Notes |
|---|---|---|
| project topic selection | student | anime topic choice |
| API source choice | student | Jikan selected for the project |
| configuration values | student with possible AI support | query, page limit, delay |
| `normalize_anime_data()` | AI assisted / AI generated | explicitly marked in notebook |
| `preprocess_anime_data()` | AI assisted / AI generated | explicitly marked in notebook |
| `run_pipeline()` | AI assisted / AI generated | explicitly marked in notebook |
| `TestAnimePipelineFunctions` | AI assisted / AI generated | explicitly marked in notebook |
| helper function docstrings | likely AI assisted | style strongly suggests AI support |
| helper functions | mixed | some may be standard patterns, some likely AI drafted |
| database schema functions | likely AI assisted | structured and template like |
| query helper functions | likely AI assisted | consistent structure and naming |
| plotting helper functions | likely AI assisted | standard but polished helper blocks |
| integration test | likely AI assisted | standard generated workflow pattern |
| Gradio interface | likely AI assisted | typical AI suggested extension |
| markdown documentation cells | likely AI generated or AI edited | highly polished and uniform |
| debugging and execution | student | notebook had to be run and fixed |
| final review and presentation prep | student | presentation and explanation decisions |


## What the Notebook Produces

When the notebook runs successfully, it may create:
- `anime_pipeline.db`
- `test_anime_pipeline.db`
- `processed_anime.csv`

These are project outputs that support storage, testing, and export of the processed dataset.

## References and Attributions

Project data source:
- Jikan REST API v4

Libraries used:
- pandas
- requests
- sqlite3
- matplotlib
- gradio
- unittest