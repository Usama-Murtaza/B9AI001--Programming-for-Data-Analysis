## Project Overview

This project implements an end-to-end **data acquisition and preprocessing pipeline** for anime metadata using the **Jikan REST API v4**. The notebook collects anime records from a public API, converts raw JSON into structured tabular data, performs preprocessing and feature engineering, loads both raw and processed datasets into **SQLite**, and supports downstream analysis through SQL queries, visualisations, automated tests, and a simple **Gradio** search interface.

The project was designed as a practical data analysis pipeline and demonstrates the full workflow from external data collection to storage, transformation, retrieval, and presentation.

## Key Features

- Public API-based data acquisition using **Jikan REST API v4**
- Search-based anime retrieval and top-anime retrieval
- JSON normalisation into a pandas DataFrame
- Data cleaning and preprocessing
- Feature engineering for score, popularity, episodes, genres, studios, and text fields
- Storage of raw and processed datasets in **SQLite**
- SQL-based retrieval and summary analysis
- Visualisations using **matplotlib**
- **Unit tests** for important helper and transformation functions
- **Integration test** for end-to-end validation
- Simple **Gradio** front end for anime title search

## Data Source

The notebook uses the **Jikan REST API v4**, a public anime API based on MyAnimeList data.

**Base URL**
```python
BASE_URL = "https://api.jikan.moe/v4"
```

### API endpoints used

- `/anime` for query-based retrieval
- `/top/anime` for top anime retrieval

### Example use cases

- Fetch anime related to a keyword such as `"naruto"`
- Fetch multiple pages of top anime data for broader analysis

## Project Structure

The notebook follows a modular pipeline design with the following stages:

1. **Package installation and imports**
2. **Configuration**
3. **Helper functions**
4. **API data acquisition**
5. **Raw JSON normalisation**
6. **Preprocessing and feature engineering**
7. **Database creation**
8. **Database loading**
9. **Database querying**
10. **Visualisation**
11. **Unit testing**
12. **Integration testing**
13. **Frontend-backend interaction**
14. **Optional summary outputs**

## Core Functions in the Notebook

### Helper and transformation functions

- `clean_text(text)`
- `safe_int(value, default=0)`
- `safe_float(value, default=0.0)`
- `classify_score_band(score)`
- `classify_popularity_band(popularity)`
- `classify_episode_group(episodes)`
- `extract_names_from_list(items)`
- `count_items_in_csv(text)`

### API functions

- `fetch_anime_search(query, max_pages=1, delay=2.0)`
- `fetch_top_anime(max_pages=1, delay=2.0)`

### Processing functions

- `normalize_anime_data(raw_anime, source_label="search")`
- `preprocess_anime_data(df)`

### Database functions

- `create_database(db_name)`
- `insert_raw_anime(df_raw, db_name)`
- `insert_processed_anime(df_processed, db_name)`

### Query and analysis functions

- `get_all_processed_anime(db_name, limit=20)`
- `search_anime_by_title(db_name, keyword)`
- `get_average_score_by_type(db_name)`
- `get_anime_count_by_year(db_name)`
- `get_top_genres(db_name, top_n=10)`
- `get_top_studios(db_name, top_n=10)`
- `get_score_band_summary(db_name)`
- `get_popularity_band_summary(db_name)`

### Pipeline and testing functions

- `run_pipeline(query=None, use_top=False, max_pages=2, db_name="anime_pipeline.db")`
- `run_unit_tests()`
- `integration_test_pipeline()`
- `gradio_search(keyword)`

## Installation

Install the required packages in Colab using:

```python
!pip -q install pandas requests matplotlib gradio
```

## Libraries Used

- `requests`
- `sqlite3`
- `pandas`
- `re`
- `string`
- `time`
- `collections.Counter`
- `datetime`
- `matplotlib`
- `unittest`
- `gradio`

## Configuration

The notebook uses the following main configuration variables:

```python
BASE_URL = "https://api.jikan.moe/v4"
DB_NAME = "anime_pipeline.db"
SEARCH_QUERY = "naruto"
MAX_PAGES = 3
REQUEST_DELAY = 1.2
```

### Notes

- `SEARCH_QUERY` controls the anime search term
- `MAX_PAGES` controls how many pages are fetched
- `REQUEST_DELAY` helps reduce rate-limit issues
- `DB_NAME` is the SQLite database file created by the notebook

## How the Pipeline Works

### 1. Data acquisition

The notebook retrieves anime data from the Jikan API using either:

- a search term, or
- the top-anime endpoint

The returned response is JSON and may contain nested structures such as genres, studios, themes, and demographics.

### 2. Normalisation

The raw API response is converted into a structured pandas DataFrame. Nested fields are flattened into comma-separated strings so they can be stored and analysed more easily.

### 3. Preprocessing

The notebook performs several preprocessing steps:

- removes duplicate anime based on `mal_id`
- cleans title, English title, and synopsis text
- converts numeric fields safely
- handles missing values
- standardises text for downstream analysis

### 4. Feature engineering

The notebook creates additional analytical features, including:

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

### 5. Database loading

Two SQLite tables are created:

- `raw_anime`
- `processed_anime`

`raw_anime` stores the original extracted metadata.

`processed_anime` stores transformed and engineered features linked back to each anime record through `mal_id`.

### 6. Analysis and retrieval

The notebook includes SQL queries to analyse:

- processed anime records
- anime by title search
- average score by type
- anime count by year
- top genres
- top studios
- score band summaries
- popularity band summaries

### 7. Visualisation

The notebook provides charts for:

- average score by anime type
- anime count by year
- top genres
- top studios

## Database Schema

### Table: `raw_anime`

Stores raw metadata from the API, including fields such as:

- `mal_id`
- `title`
- `title_english`
- `type`
- `source`
- `episodes`
- `status`
- `score`
- `popularity`
- `members`
- `favorites`
- `synopsis`
- `rating`
- `year`
- `season`
- `genres`
- `themes`
- `studios`
- `demographics`
- `url`
- `fetched_at`

### Table: `processed_anime`

Stores cleaned and engineered fields such as:

- `mal_id`
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

## Running the Notebook

### Option 1: Search-based retrieval

```python
df_raw, df_processed = run_pipeline(
    query=SEARCH_QUERY,
    use_top=False,
    max_pages=MAX_PAGES,
    db_name=DB_NAME
)
```

### Option 2: Top anime retrieval

```python
df_raw, df_processed = run_pipeline(
    use_top=True,
    max_pages=MAX_PAGES,
    db_name=DB_NAME
)
```

## Outputs Generated

After execution, the notebook produces:

- a raw anime DataFrame
- a processed anime DataFrame
- an SQLite database file: `anime_pipeline.db`
- a CSV export: `processed_anime.csv`
- charts and tables for analysis
- test outputs from unit and integration tests

## Testing

### Unit tests

The notebook includes unit tests for the main helper and transformation functions. These tests confirm that:

- text cleaning behaves as expected
- score bands are classified correctly
- popularity bands are classified correctly
- episode groups are assigned correctly
- list extraction functions work properly
- comma-separated counts are calculated correctly

### Integration test

The integration test validates the full pipeline:

1. fetch data from the API
2. normalise the raw data
3. preprocess the data
4. create the test database
5. insert raw and processed records
6. retrieve the inserted records successfully

## Frontend-Backend Interaction

A simple Gradio interface is included to demonstrate search functionality over the SQLite database.

### Gradio function

```python
def gradio_search(keyword):
    ...
```

### Launch in Colab

```python
demo.launch(share=True)
```

This provides a small frontend where a user can search anime titles and receive matching results from the stored database.

## Example Analytical Questions This Notebook Can Answer

- What are the most common anime genres in the dataset?
- Which studios appear most frequently?
- How does average score vary by anime type?
- How many anime records appear per year?
- How many anime fall into each score band?
- How many anime fall into each popularity band?

## Strengths of the Notebook

- Clear modular pipeline design
- Practical API-based workflow
- Both raw and processed data are preserved
- Includes database storage instead of DataFrame-only analysis
- Includes automated tests
- Includes a simple interactive interface
- Easy to extend with additional queries or visualisations

## Limitations

- Results depend on what the API returns at the time of execution
- Search-based queries may bias the dataset toward a specific franchise or keyword
- Popularity and score reflect platform-level user behaviour, not objective quality
- Some metadata fields may be missing or incomplete
- Jikan is a public community-facing API, so temporary request limits may affect repeated runs

## Suggested Improvements

Future versions of the project could include:

- broader search coverage across multiple themes or franchises
- scheduled or repeated data collection over time
- additional visualisations
- comparison of seasonal anime trends
- recommendation-oriented analysis
- export of results to a dashboard or web app

## File Produced by the Notebook

The notebook exports the processed dataset as:

```text
processed_anime.csv
```

This can be used for further analysis, reporting, or presentation.

## Attribution

This project uses:

- **Jikan REST API v4** for anime metadata
- Open-source Python libraries including pandas, requests, matplotlib, gradio, and unittest

