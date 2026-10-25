# Content based movie recommendation program built using Scikit-Learn and Pandas
## What this program does
This program asks the user to input a movie that they rate highly, and will return 10 other movies that the user is likely to enjoy, using a TF-IDF vectoriser and the cosine similarity function.

## Prerequisites
Requires Python to be installed with the following libraries:
* Pandas (`pandas`)
* NumPy (`numpy`)
* Scikit-Learn (`scikit-learn`)

## Datasets
This project uses the MovieLens dataset, namely:
* **`movies.csv`**: Contains movie IDs, titles, and genre strings.
* **`ratings.csv`**: Included for future collaborative filtering expansion.

## How to Run
1. Ensure `movies.csv` and `ratings.csv` are in your project directory.
2. Run the script or Jupyter notebook:
   ```bash
   python movie_recommender.py
## Overview of the main code 
### Fetching and processing the data 

#### Data Preprocessing & Cleaning
* **Malformed Data Handling:** Load in `ratings.csv` with `on_bad_lines='skip'` to ignore misformatted rows without the program returning an error.


* **Normalising the Inverted Titles:** MovieLens has organised the titles of films to have articles after the rest of the title, for example "Wild, The (2006)", we invert this back for the sake of readability in the output to the user.

* **Regex:**We strip punctuation, symbols and unnecessary whitespace to make looking up things easier.

### Key Modelling and Engineering concepts
* **Feature Fusion:** Combines movie titles and cleaned genre strings into a single `features` column.
* **TF-IDF Vectorizer:** We use `TfidfVectorizer(stop_words='english')` to transform text features into weighted numerical frequency matrices, prioritising unique word descriptions.
* **Cosine Similarity Matrix:** Compute high similarity scores across the entire dataset in advance, so that our lookups can be near instant.

### Interactive User Interface 
* **Continuous Loop:** Built inside a `while` loop, allowing you to search multiple films in a single session without restarting the program.
* **Handling Partial Matches:** Handles case sensitivity and includes substring matching so partial matches (like typing `"toy story"`instead of `"Toy Story (1996)"`) still find the correct dataset entry.
* **Closing the Application:** Simply input `quit` or `exit` to safely close the application at any time.

## Core Algorithm & Recommendation Logic
The program has 3 main stages:
1. **Vectorisation & Similarity:** We combine titles and genres, transform them using `TfidfVectorizer`, and in advance compute a **cosine similarity matrix**.
2. **Mapping Indices:** We initialise an `indices` series that maps clean, lowercase titles to their respective row numbers in the sorted DataFrame, ensuring fast O(1) lookups.
3. **Retrieving similar movies and ranking them:** When a user inputs a movie, the `get_recommendations()` function executes these steps:
   - Cleans input string via regex to match the dataset's format
   - Looks up the movie's row index (`idx = indices[title]`).
   - Extracts and sorts all similarity scores in descending order using `enumerate()`.
   - Takes the top 10 indices, maps them back to the original DataFrame titles, and returns them as a clean Python list via `.tolist()`.