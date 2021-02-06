## Exercise 1 -- Analyzing Gapminder Data

### Exercise 1A

The purpose of this first exercise was to get a list of all the years in the provided dataset, without any
duplicates, and figure out how many unique values there were. I thought of two approaches that could work: casting
the dataframe's **year** column to a list type and operating on that, or using the unique() function. In the latter approach,
I declared and initialized a variable to the value of indexing the given data according to the year variable like so `unique_year = data['year'].unique()` and I 
found the length of `unique_year` by `print(len(unique_year))`. This is far more efficient compared
to my former approach, which was to get all the years out of the given data using the **year** 
column variable and convert it to a list with `year = data['year'].to_list()`. Once I had a list, I iterated over the list
to find which values were unique and stored them in a separate uninitialized list (`temp`) using list comprehension like so: `[temp.append(year) for year in year if year not in temp]`.
The unique() approach has better runtime, and requires less storage, so I think that's the better solution to choose out of the two I came up with.

### Exercise 1B

The purpose of the second exercise was to find the largest population in the given dataset, and find out when and where
this occurred. I found the largest population by indexing the given dataset based on the column variable **pop** and 
using the max() function to find the maximum population in the given dataset; `largest_pop_idx = data['pop'].idxmax()`. After
`largest_pop_idx` was initialized I declared and initialized another variable to use the boolean dataframe returned
by `largest_pop_idx` called `where_and_when`. I called iloc() on `where_and_when` with `largest_pop_idx` as iloc()'s argument
in order to get the information on the country where the largest population occurred. However, I still had to index the single dataframe
in order to get the country name and year. I did this by indexing my `where_and_when` data frame; 
```python
country = where_and_when['country']
year = where_and_when['year']
print(f'\nThe max population occured in {country} during the year {year}.')
```
This gave me both the country and year for where and when the largest population in the given dataset occurred.

### Exercise 1C

The purpose of the third exercise was to extract all records for Europe and find out which country has the smallest population
in the year 1952, and what was the population of that country in 2007. My goal with this exercise was to keep it general so that
it could be refactored into a function if need be. In order to do this, I declared and initialized three variables and the 
beginning of my program:
```python
cont = 'Europe'
y1 = 1952
y2 = 2007
```
From here, everything is based on those variables. Hard-coding the variables inside the rest of my code would have been fine
for the purpose of this exercise, but would be a headache later if I needed to reuse the code. 

After declaring and initializing my variables, I extracted all continents matching Europe from the given dataset with these two
lines: 
```python
cont_idx = (data['continent'] == cont)
data_cont = data[idx]
```
`data_cont` is a dataframe with all the information about European countries for all years, so now I had to refine the `data_cont` 
dataframe by the two years I was given. I did this for both years with these two lines: 
```python
data_filtered_y1 = data_cont[data_cont['year'] == y1]
data_filtered_y2 = data_cont[data_cont['year'] == y2]
```
With these two lines I accomplished four steps. I indexed the `data_cont` dataframe, got back a boolean dataframe (only true if
the **year** matched), and compared the boolean dataframe to the `data_cont` dataframe to get a new dataframe for the two years provided. 
Now I had two Europe dataframes for `y1` and `y2`. After getting those two dataframes, I found the lowest population using the idxmin()
function (applying this to both dataframes). Once I had the index, I used loc() with the lowest population index return value as the
argument and received Iceland as the answer, with 1952's population being 147962 individuals and 2007's population being 301931 individuals.