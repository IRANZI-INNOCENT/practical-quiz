# DSA 4060 Personalized Movie Recommender

## Student Details
- Name: Iranzi Innocent
- Student ID: 670513
- Assigned User ID: 14

The assigned user is calculated from the last two digits of the Student ID: (13 MOD 40) + 1 = 14.

## Project Objective
This project builds a simple content-based movie recommender for one assigned viewer. It uses that user's rating history to identify preferred genres, then ranks unseen catalogue movies by how similar their genres are to the movies the user rated 4.0 or higher. The output is a Top 5 list with a reason for each title.

## Datasets
- `movies.csv`: 36 movies with `movie_id`, `title`, and pipe-separated `genres`.
- `ratings.csv`: 440 explicit ratings from 40 users, with `user_id`, `movie_id`, and `rating` (1.5 to 5.0).

Both files were supplied for the practical quiz and are included in this repository.

## Method / Approach
1. Filter `ratings.csv` to User 14 and join the movie titles and genres.
2. Treat ratings of 4.0 or higher as liked movies. For User 14 those films are *The Matrix* (Sci-Fi|Action) and *Avengers: Endgame* (Action|Superhero).
3. Convert the genre strings into numerical features with TF-IDF, treating each genre tag as a token.
4. Build a user profile as the mean TF-IDF vector of the liked movies.
5. Rank every other catalogue movie by cosine similarity to that profile.
6. Remove movies User 14 has already rated and return exactly five titles.

## How to Run the Notebook
Required tools: Python 3, Jupyter, pandas, scikit-learn, and matplotlib.

```text
pip install pandas scikit-learn matplotlib jupyter
```

1. Open `DSA4060_Recommender_670513.ipynb` from this folder.
2. Run all cells from top to bottom. The notebook reads `movies.csv` and `ratings.csv` from the same directory.

## Recommendation Results
For User 14 the five recommended movies are:

1. Mission: Impossible - Fallout
2. Mad Max: Fury Road
3. Sherlock Holmes
4. Interstellar
5. Spider-Man: Into the Spider-Verse

The list is driven by Action, Sci-Fi, and Superhero overlap with the two liked films. None of the five titles appears in User 14's rating history. Drama, Romance, and Sports, which this user scored lowest, do not lead the ranking.

## Limitation and Suggested Improvement
A limitation is that the profile is built from only two liked movies and from genre tags alone, so two Action films are treated as similar even when tone, cast, and story differ. A realistic improvement is to weight each liked movie by its rating, or to add a second signal such as director, franchise, or ratings from users with a similar Action-and-Sci-Fi history.
