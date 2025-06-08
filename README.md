# Netflix_Analysis_Python


## Overview
This project analyzes Netflix’s content library using Python and Matplotlib, extracting insights through visualizations. It examines content distribution, ratings, durations, release trends, and country-wise contributions.

## Dataset
The analysis is based on `netflix_titles.csv`, containing details about movies and TV shows available on Netflix, such as type, release year, rating, country, and duration.

## Dependencies
Install the required libraries:
```bash
pip install pandas matplotlib
```

## Data Cleaning
The dataset is cleaned by removing missing values from key columns: `type`, `release_year`, `rating`, `country`, and `duration`.

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('netflix_titles.csv')
df = df.dropna(subset=['type', 'release_year', 'rating', 'country', 'duration'])
```

## Visualizations and Insights
### 1. Movies vs. TV Shows on Netflix
A bar chart comparing the number of movies and TV shows available.

```python
type_counts = df['type'].value_counts()
plt.figure(figsize=(6,4))
plt.bar(type_counts.index, type_counts.values, color=['skyblue', 'orange'])
plt.title('Number Of Movies VS TV Shows On Netflix')
plt.xlabel('Type')
plt.ylabel('Count')
plt.tight_layout()
plt.savefig('movies_vs_tvshows.png')
plt.show()
```

### 2. Content Rating Distribution
A pie chart illustrating the percentage of different content ratings.

```python
rating_counts = df['rating'].value_counts()
plt.figure(figsize=(8,6))
plt.pie(rating_counts, labels=rating_counts.index, autopct='%1.1f%%', startangle=90)
plt.title('Percentage OF Content Rating')
plt.tight_layout()
plt.savefig('Content_rating.png')
plt.show()
```

### 3. Movie Duration Distribution
A histogram showing the distribution of movie durations.

```python
movie_df = df[df['type'] == 'Movie'].copy()
movie_df['duration_int'] = movie_df['duration'].str.replace('min', '').astype(int)

plt.figure(figsize=(8,6))
plt.hist(movie_df['duration_int'], bins=30, color='purple', edgecolor='black')
plt.title('Distribution of Movie Duration')
plt.xlabel('Duration (minutes)')
plt.ylabel('Number Of Movies')
plt.tight_layout()
plt.savefig('movie_duration_hist.png')
plt.show()
```

### 4. Release Year vs. Number of Shows
A scatter plot analyzing how Netflix's catalog has grown over time.

```python
release_counts = df['release_year'].value_counts().sort_index()
plt.figure(figsize=(10,6))
plt.scatter(release_counts.index, release_counts.values, color='red')
plt.title('Release Year VS Number Of Shows')
plt.xlabel('Release Year')
plt.ylabel('Number Of Shows')
plt.tight_layout()
plt.savefig('release_year_scatter.png')
plt.show()
```

### 5. Top 10 Countries by Number of Shows
A horizontal bar chart ranking the top 10 contributing countries.

```python
country_counts = df['country'].value_counts().head(10)
plt.figure(figsize=(8,6))
plt.barh(country_counts.index, country_counts.values, color='teal')
plt.title('Top 10 Countries By Number Of Shows')
plt.xlabel('Number Of Shows')
plt.ylabel('Country')
plt.tight_layout()
plt.savefig('top_10_country.png')
plt.show()
```

### 6. Movies and TV Shows Released Over Years
A side-by-side line plot comparing the yearly trend for movies and TV shows.

```python
content_by_year = df.groupby(['release_year', 'type']).size().unstack().fillna(0)

fig, ax = plt.subplots(1,2, figsize=(12,5))

# First subplot: Movies
ax[0].plot(content_by_year.index, content_by_year['Movie'], color='blue')
ax[0].set_title('Movie Release Per Year')
ax[0].set_xlabel('Year')
ax[0].set_ylabel('Number of Movies')

# Second subplot: TV shows
ax[1].plot(content_by_year.index, content_by_year['TV Show'], color='green')
ax[1].set_title('TV Shows Release Per Year')
ax[1].set_xlabel('Year')
ax[1].set_ylabel('Number of TV Shows')

fig.suptitle('Comparison of Movies and TV Shows Released Over Years')

plt.tight_layout()
plt.savefig('movies_tv_shows_comparison.png')
plt.show()
```

## How to Run
1. Place `netflix_titles.csv` in the working directory.
2. Run the script:
   ```bash
   python analysis.py
   ```
3. View the generated plots in the output directory.

## Conclusion
This analysis provides valuable insights into Netflix’s content trends, distribution, and growth over the years.

