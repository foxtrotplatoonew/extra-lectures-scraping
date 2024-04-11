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


# Helpful Docs
- [requests](https://requests.readthedocs.io/en/latest/)
- [beautiful soup](https://beautiful-soup-4.readthedocs.io/en/latest/#)
- [pandas](https://pandas.pydata.org/docs/)
- [jupyter](https://docs.jupyter.org/en/latest/)


# Other helpful resources
- [Corey Schafer Requests](https://www.youtube.com/watch?v=tb8gHvYlCFs&t=87s)
- [Corey Schafer Beautiful Soup](https://www.youtube.com/watch?v=ng2o98k983k&t=202s)
- [Tech with Tim Web Scraping](https://www.youtube.com/watch?v=gRLHr664tXA&t=270s)



