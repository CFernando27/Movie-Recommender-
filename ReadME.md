# Content based movie recommendation program built using Scikit-Learn and Pandas
## What this program does
This program asks the user to input 5 movies that they rate highly, and using a cosine similarity function that takes into account titles and genres via a TF-IDF vectoriser, will return 5 other movies that the user is likely to enjoy.

### The Recommendation Function
We use the cosine similarity function to take a movie and return the 10 movies from the dataset which are most similar to it. Before this, we initialise a variable *indices* which is a pandas series that stores a film's index under its title. 

Hence in the function we can fetch the index of the input movie with 
```
idx = indices[title]
```

The function uses the movie's row index to extract all similarity scores from the cosine_sim matrix. Then, we pair each score with its respective movie index using enumerate(), and sort them in descending order of similarity score.

For these films, we extract their row indices, look up their titles in the original DataFrame, and convert the final output into a clean Python list using **.tolist()**

