# Extra Lecture -- Intro to Web Scraping

In this extra lecture, the goal is to introduce some libraries that can help with collecting and manipulating data for a project. By the end of this lecture we will:
    
- Use requests to get HTML documents from the web
- Use beautiful soup to parse HTML in python
- Use pandas to persist our scraped data in a dataframe and CSV
- Use Jupyter Notebook to interact with our dataframe and CSV data
- Build a Django Fixture with our scraped Data
- Load our fixture into a Django Postgres Database


The [exercise](#getting-started-with-requests-and-beautiful-soup-scraping-exercise-1) for getting started with beautiful soup and requests is meant to help you work through understanding how to use beautiful soup and requests together. When you feel comfortable that you can collect data you are interested in, try collecting some data YOU are interested in.



We will briefly work with the following libraries in python for this lesson:

- Requests
- Beautiful Soup
- Jupyter
- Pandas

Its worth noting that this exercise can be completed with just the use of Requests and Beautiful Soup, but Jupyter and Pandas offer some helpful convenient ways to interact with our data. There are also other tools that can be used for this, so do not feel limited to the listed libraries above, there are many ways to collect and manipulate data!


# What is Web Scraping?

At a basic level web scraping is a technique for collecting data from websites. So how does it work?

It usually involves using some tools that allow you to manipulate and transform `html documents`

In `python` we will accomplish this with `requests` and `beautiful soup`:
- `requests` allow us to `GET` html documents
- `beautiful soup` allows us to `parse` html in python

Together this provides us with a powerful way to collect data in which `requests` lets us grab large amounts of HTML, and `beautiful soup` helps filter down the HTML to our desired results




### Getting Started with Requests and Beautiful Soup, Scraping Exercise 1

Installing Requests and Beautiful Soup:

Requests
```
pip install requests
```

Beautiful Soup
```
pip install beautifulsoup4
```

1. Use the requests library to make a request to `http://quotes.toscrape.com`
2. How can you get requests to give you the data you requested as html?
<details>
  <summary>Hint #1</summary>
  <p>use the dir() method on the variable that stores your request, what methods are available?</p>
</details>

<details>
  <summary>Hint #2</summary>
  <p>Using the requests documentation, are there any methods that can help us get the html content from the request?</p>
</details>

3. Use beautiful soup to parse the html from your request
4. Can you get a list of quotes and their corresponding authors?
5. Notice this is just the first page
<details>
  <summary>Hint #3</summary>
  <p>What happens if you click the next button? Does your url appear to change?</p>
</details>

<details>
  <summary>Hint #4</summary>
  <p>Is there a pattern to how the next pages form their url's?</p>
</details>
6. What Author has the most quotes from the first 10 pages?


## Creating a Movie API

This will be the example we go over in class.

We will:
1. Use `requests` to get an HTML document that contains movie data we are interested in
2. Use `beautiful soup` to parse that HTML data in python
3. Use `pandas` to conveniently manipulate our data we have parsed
4. Use `jupyter notebook` to help visualize the data we manipulate with pandas
5. Write a `script` that takes our data and creates a `fixture` that can be used by `django`


At this point you should be able to create a django project, that uses this fixture to load data in your postgres database.

You will:
1. Make a django view that uses the data you have collected
<details>
  <summary>Hint: Lecture on Django Fixtures</summary>
  <p>Check out <a href="https://www.youtube.com/watch?v=m6uUh-oi8fI">Django Fixtures Lecture</a> if you need some help creating an API in django with a fixture</p>
</details>


Can you use this data in an application that has CRUD features? (stretch goal)


- Installing dependencies

install requests
```
pip install requests
```

install beautiful soup
```
pip install beautifulsoup4
```

install pandas
```
pip install pandas
```

install jupyter
```
pip install jupyter
```


The url that we will be using to create this Movie API is:

`https://www.imdb.com/chart/top/`


An example of some headers you may want to include in requests are:

```
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36'
}
```

Follow along in class if you can, don't worry if you have trouble running some commands or keeping up with the pace of the lecture. There are a lot of new things being introduced here, so it is very normal for it to take some time to understand how to best use the tools together.


### Help with Getting Started on Exercise 1
If you have already looked at some of the requests documentation and beautiful soup documentation, but still are having trouble getting started go ahead and use some of the code below to get started:

```
from bs4 import BeautifulSoup
import requests


target_html_page = requests.get('http://quotes.toscrape.com')

soup = BeautifulSoup(target_html_page.text, 'html.parser')

quotes = soup.findAll('span', attrs={'class': 'text'})

authors = soup.findAll('small', attrs={'class':'author'})

for quote, author in zip(quotes, authors):

print(f'{quote.get_text()} --{author.get_text()}')

```

Add some print statements in and make sure you understand what we are targeting here.
1. We are getting all the html for a given page
2. We are then filtering by the type of tag, and the class name
3. We are iterating over our tags and extracting the text
4. We are printing a formatted string with some data we may be interested in

- See if there are other things you can target, consider how you might want to arrange your data

Can you collect data that answers the following questions?
How many quotes are in the first 10 pages?
Who has the most quotes in the first 50 pages?
What is the longest quote in the first 25 pages?
Is there a quote in pages 26-50 larger than the longest quote in the first 25 pages?

Okay, thats a good amount. If you feel that was easy it sounds like you can confidently move on to trying to collect data that may be harder to get.

If you are having trouble with the exercises, look through the documentation and research strategies to locate your desired data, practice goes a long way.


### Exercise 2

If you are wanting to try and follow allong with the code from lecture, this code will be helpful for getting to the point of creating your fixture.

- Goals from lecture:
  - Become familiar with requests
  - Become familiar with beautiful soup
  - Become familiar with jupyter
  - Become familiar with pandas
I think its safe to say we have at least gotten some exposure to these topics.
  - Scrape data that we can use for an API
  - Use pandas to manipulate data we have scraped
  - Use jupyter to interact with and visualize our data we have scraped
  - Create a json fixture that can be used by a django project

These goals are very general on purpose. If possible, it would be strongly encouraged research a website from which you can properly collect data from to use in your own project.

A lot of that research can be time intensive, depending on how complicated the task is you are setting out to do. You can still practice a lot of generalized simpler versions of scraping, to make sure you have a good understanding of how to easily collect data from the web.

So in a perfect scenario, you would actually complete Exercise 2 with your own website, collecting data you would like to use in a personal or group project maybe in the future.

But for those who are still wanting to practice, or have not quite decided what kind of data they wish to collect, the code below is what we used in lecture.

1. Importing requests, beautiful soup, pandas, and json (must pip install requests, beautifulsoup4, pandas, jupyter)
```
import requests
from bs4 import BeautifulSoup
import pandas as pd
import json
```

2. Check that we can get html content from desired webpage

```
url = 'https://www.imdb.com/chart/top/'

headers = {'user-agent': 'my-app/0.0.1'} #May not always be needed but is for this url

html_content = requests.get(url, headers=headers) #Pass in headers with request

soup = BeautifulSoup(html_content.text, 'html.parser')
print(soup)
```

Here you could print `html_content.text` or `soup`, we mainly want to check that we are getting a page of HTML (Otherwise soup can't do a lot of work for us)

3. If you are getting html_content, now see if you can get the h3 tags that have our title data

Check and see that we are printing what looks like our movie titles
```
titles = soup.find_all('h3', class_='ipc-title__text')
print(titles)

### print to see inner text of h3 tags
# for title in titles:
#   print(title.text)

```

4. From observing the way our data was being parsed, we came up with a way to get just the rank and title data from our h3 elements

- Get rid of the print statements and for loop that prints inner text
- Place the following after `titles = soup.find_all('h3', class_='ipc-title__text')`

```
ranks = []
movie_titles = []

for title in titles:
    try:
        rank, movie_title = title.text.split('.',1)
        ranks.append(rank)
        movie_titles.append(movie_title)
    except ValueError:
        continue

print(ranks)
print(movie_titles)
```

At this point you should be able to verify that your ranks and movie_titles list do in fact print lots of data. An easier way to look at this data would be in a CSV or jupyter notebook.. so lets do both.

5. Writing ranks and movie_titles to a csv

```
## Creating a data frame for ranks and movie titles
df_ranks = pd.DataFrame({"rank": ranks})
df_titles = pd.DataFrame({"title": movie_titles})
# Writing the dataframes to csv
df_ranks.to_csv('ranks.csv', index=False)
df_titles.to_csv('titles.csv', index=False)
```

6. If you have CSV's with data, you should now be in the clear to launch jupyter notebook by typing `jupyter notebook` from your terminal.

This should launch a jupyter notebook where you will want to create a new notebook and select Python3.
- When you get into your jupyter notebook, go ahead and run `ls` in the first cell

This should display your python files including your CSV's

You likely won't have to move, but if you perhaps put your CSV's in another folder, just `cd` into that folder to easily target the CSV

- Commands to run in jupyter

Need to import pandas
```
import pandas as pd 
```

Create data frame for ranks and titles from the csv data we made
```
df_titles = pd.read_csv('titles.csv')
df_ranks = pd.read_csv('ranks.csv')
```

We can check to see what these look like with:

Checking Titles
```
df_titles
```

Checking Ranks
```
df_ranks
```

At this point you may notice some columns or rows are getting truncated. In our case it will likely be rows. This is a way we can change that:

Removing limit of max rows for dataframes
```
pd.set_option('display.max_rows', None)
```

Note that we can do the same thing with `max_columns` but this will not apply to us for this exercise.

- If the above data looks good in Jupyter
  - The data appears to be valid
  - We have the correct number of entries

Then we will go ahead and try and combine our data:

Combining dataframes through pd.concat, and write to csv
```
df_ranks_titles = pd.concat([df_ranks, df_titles], axis=1)

# Write the verified data to the csv
df_ranks_titles.to_csv('movie_db.csv')
```

7. At this point we have a csv with just movie_titles and ranks.
- You can remove previous code all the way until we reach `titles = soup.find_all('h3', class_='ipc-title__text')`

We basically are going to rewrite our loop. Don't worry your CSV data for ranks and titles are still good, we just are now performing work to find the a tags that include our movie data within our for loop.

```
ranks = []
movie_titles = []
release_years = []
movie_lengths = []
movie_ratings = []

for title in titles:
    try:
        rank, movie_title = title.text.split('.',1)
        ranks.append(rank)
        movie_titles.append(movie_title)
    except ValueError:
        continue
    
    #Find the next div from the current title
    next_div = title.find_next('div')
    #Get all of the spans within the div
    spans = next_div.find_all('span', class_='cli-title-metadata-item')
    
    for index, span in enumerate(spans):
        if index == 0: #year
            release_years.append(span.get_text(strip=True))
        elif index == 1: #movie length
            movie_lengths.append(span.get_text(strip=True))
        elif index == 2: #rating
            movie_ratings.append(span.get_text(strip=True))
    

print(release_years)
print(movie_lengths)
print(movie_ratings)


df_years = pd.DataFrame({"year": release_years})
df_lengths = pd.DataFrame({"length": movie_lengths})
df_ratings = pd.DataFrame({"rating": movie_ratings})

df_years.to_csv('release_years.csv', index=False)
df_lengths.to_csv('movie_lengths.csv', index=False)
df_ratings.to_csv('movie_ratings.csv', index=False)   
```

The print statements should let us know that `release_years`, `movie_lengths`, and `movie_ratings` contain data.

We similarly load in our lists to create data frames.

And after we create our dataframes we write CSV's of our data.

## Stretch Goal
So as I mentioned in lecture, we can quickly see if we look at the movie_ratings dataframe or CSV, that we are missing some entries.

It turns out that some ratings are missing from the IMDB data. Luckily it was only a few entries, so you can actually compare your csv data to the website data, and there are only a couple entries to fix.

But can we come up with a better solution? Surely there is a way to determine that if `elif index == 2: #rating` does not exist, we could handle this to preserve the order?

Maybe we could also collect our data differently.

Can you come up with a way to run the script so that no human interaction is needed to create the fixture?

In otherwords can you run the script once and successfully get a fixture that includes ranks, movie_titles, release_years, movie_lengths, and movie_ratings?


- For simplicity sake, if you do not have time to take on the challenge of the stretch goal, just go ahead and make your `ratings.csv ` contain the proper number of rows to be concatenated

8. Visualize your data and combine into a final csv to be used for your fixtures

Perform these in jupyter notebook
```
#Read in your data and create dataframes
df_release_years = pd.read_csv('release_years.csv')
df_movie_lengths = pd.read_csv('movie_lengths.csv')
df_movie_ratings = pd.read_csv('movie_ratings.csv')

#Get movie db or at least current state of movie_db
df_movie_db = pd.read_csv('movie_db.csv', index_col=False)
#concat movie db to get all data together
df_movie_db = pd.concat([df_movie_db, df_release_years, df_movie_lengths, df_movie_ratings], axis=1)
### Check dataframe
df_movie_db
#Writing to csv to update db data
df_movie_db.to_csv('movie_db', index=False)
```

9. Use the CSV you built from scraping

Example of writing a for loop to create fixture data

```
import requests
from bs4 import BeautifulSoup
import pandas as pd
import json

df_movie_db = pd.read_csv('movie_db.csv')

fixtures = []
pk = 1

for index, row in df_movie_db.iterrows():
    fixture = {
        "model": "movies.Movie",
        "pk": pk,
        "fields": {
            "rank": row['rank'],
            "title": row['title'],
            "year": row['year'],
            "length": row['length'],
            "rating": row['rating'],
        }
    }
    fixtures.append(fixture)
    pk += 1
    
with open('movie_fixture.json', 'w') as json_file:
    json.dump(fixtures, json_file, indent=4)
```

- Things you need to use your fixture:
  - [] Django project with an app `movies`
  - [] pk needs to properly auto increment for your fixtures
  - [] `fields` needs to contain all of the fields for your `model`(Movie)
  - [] fixture needs to be a json object

Lets say you have a project `movies_db` with an app `movies` that contains `Movie` model.

You are in good shape, now you just need to make sure your Movie model has the fields `rank`,`title`, `year`, `length`, `rating`

You now should be able to load the data into your database by placing your fixture in a fixtures folder.

In side your `movies` app, can create a new directory `fixtures`

Lets say you named your fixture `imdb_movie_data.json`

Place your fixture in the fixtures directory (/movies/fixtures/imdb_movie_data.json)

You can now run `python manage.py loaddata imdb_movie_data`

If done successfully you will get a success message letting you know that you loaded (x) number of objects into the database



# Helpful Docs
- [requests](https://requests.readthedocs.io/en/latest/)
- [beautiful soup](https://beautiful-soup-4.readthedocs.io/en/latest/#)
- [pandas](https://pandas.pydata.org/docs/)
- [jupyter](https://docs.jupyter.org/en/latest/)


# Other helpful resources
- [Corey Schafer Requests](https://www.youtube.com/watch?v=tb8gHvYlCFs&t=87s)
- [Corey Schafer Beautiful Soup](https://www.youtube.com/watch?v=ng2o98k983k&t=202s)
- [Tech with Tim Web Scraping](https://www.youtube.com/watch?v=gRLHr664tXA&t=270s)



