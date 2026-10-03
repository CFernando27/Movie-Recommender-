# Notes from Movie Recommendation program

## Pre processing and reading stage 
```
print(movies_df[movies_df['title'].str.contains('Toy Story', na = False)])
```
* movies_df[] gives the actual row, without it you just get T/F
* na = False means it ignores inputs where there's nothing in the rows

```
movies_df['sort_key'] = movies_df['title'].str.replace(r'[^a-zA-Z0-9\s]', '', regex=True).str.lower().str.strip()
```

* this creates a dummy column with the same titles, but removes all of the special characters. ^ means not - so not a-z,A-Z,0-9 or whitespace.
Then we can sort alphabetically by doing....

```
movies_sorted = movies_df.sort_values(by = 'sort_key' , ascending = True)
```
Or do ascending = False for reverse alphabetical.
