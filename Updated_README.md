# Anime Metadata, Genre, and Popularity Trend Analysis Pipeline

## Project Summary

This project builds a complete data acquisition and preprocessing pipeline for anime metadata using a public API. The notebook collects anime data from the Jikan REST API, converts the raw JSON into a tabular format, cleans and transforms the data, stores both raw and processed records in a SQLite database, runs queries and visual analysis, and includes testing and a simple search interface.

The main notebook file for this project is `Anime_updated.ipynb`.

This README is a authorship audit.

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

## Full AI and Authorship Audit

This section is a stricter audit of the notebook. It is based on:
- explicit comments already inside the notebook
- the structure and style of the code
- the style and tone of markdown cells
- the level of polish and consistency across sections

This section does not claim certainty where certainty is not possible. It identifies what should reasonably be declared as AI generated or AI assisted based on the notebook itself.

## Parts Clearly Marked in the Notebook as AI Written

1. `normalize_anime_data()`
   - notebook comment says the logic was self devised and the code was AI written for efficiency

2. `preprocess_anime_data()`
   - notebook comment says the logic was self devised and the code was AI written for efficiency

3. `run_pipeline()`
   - notebook comment says the code was AI written for efficiency

4. `TestAnimePipelineFunctions`
   - notebook comment says this test class was written by AI


### 1. Most markdown or documentation cells

This includes:
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

This applies to:
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


### 6. Gradio interface section
The frontend block is a AI suggested extension for demonstrating frontend and backend interaction.

This includes:
- `gradio_search()`
- `gr.Interface(...)`


### 7. Integration test structure
The unit test class & integration test is AI written:
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

## What the Notebook Produces

When the notebook runs successfully, it creates:
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