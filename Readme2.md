## Phase 1 Project Submission

Please fill out:
* Student name: Hellen Mwangi
* Student pace:part time 
* Scheduled project review 16/4/2023/00.00am: 
* Instructor name: Noah Kandie
* Blog post URL:
  

# Microsoft Movie Studio Venture Project




# Overview


This project helps to explore relationships between  budget, genre, rt_movies average ratings score, and ROI.On this project four datasets will be used for analysis, ie tmbd_movies,tn_movies,rt_movies and bom_movies.Bes option of studios is also in place to guide more on which studios to use to market the movies.Commedy,drama ,comedy/drama,drama/mystery and suspense appears to be the most popular.In terms of ROI the correlation is positive in that as genres are being put together they perform better but it depends of whats put together.Eg dramas seem to sell more .


# Business Problem.
Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. You are charged with exploring what types of films are currently doing the best at the box office. You must then translate those findings into actionable insights that the head of Microsoft's new movie studio can use to help decide what type of films to create.

# Variables Used .
1. Return investment
2. Genre that is most prefered
3. Movie ratings and vote average



# The Research Questions. 

1. Which genre is the most prefered by a large audience?
2. Which genre has the greatest return investment if they need to venture in this movie business?
3. Which movie genre has the highest ratings?


# DATASETS PROVIDED FOR THE PROJECT.

the folder zippedData are movie datasets from:

1. Box Office Mojo.
2. IMDB. 
3. Rotten Tomatoes.
4. TheMovieDB. 
5. The Numbers.

# DATASETS USED FOR THE PROJECT ANALYSIS AND VISUALIZATION OF DATA.

NB. after opening the above data the below were used for the project.
1. bom.movie_gross.csv
2. tn_movies.csv
3. tmdb.movies.csv
4. rt_movies.csv



# DATA UNDERSTANDING.





## Exploring Data From The given Datasets.



```python
# Your code here - remember to use markdown cells for comments as well!
# importing all relevant alias
import pandas as pd
import csv 
import sqlite3
import matplotlib.pyplot as plt
%matplotlib inline
import numpy as np
import seaborn as sns
```


```python
# viewing first 5 entries
bom_df = pd.read_csv('zippedData/bom.movie_gross.csv.gz')
bom_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>studio</th>
      <th>domestic_gross</th>
      <th>foreign_gross</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Toy Story 3</td>
      <td>BV</td>
      <td>415000000.0</td>
      <td>652000000</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alice in Wonderland (2010)</td>
      <td>BV</td>
      <td>334200000.0</td>
      <td>691300000</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Harry Potter and the Deathly Hallows Part 1</td>
      <td>WB</td>
      <td>296000000.0</td>
      <td>664300000</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inception</td>
      <td>WB</td>
      <td>292600000.0</td>
      <td>535700000</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Shrek Forever After</td>
      <td>P/DW</td>
      <td>238700000.0</td>
      <td>513900000</td>
      <td>2010</td>
    </tr>
  </tbody>
</table>
</div>




```python
bom_df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>domestic_gross</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3.359000e+03</td>
      <td>3387.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2.874585e+07</td>
      <td>2013.958075</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.698250e+07</td>
      <td>2.478141</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000e+02</td>
      <td>2010.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.200000e+05</td>
      <td>2012.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.400000e+06</td>
      <td>2014.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.790000e+07</td>
      <td>2016.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>9.367000e+08</td>
      <td>2018.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
bom_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3387 entries, 0 to 3386
    Data columns (total 5 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   title           3387 non-null   object 
     1   studio          3382 non-null   object 
     2   domestic_gross  3359 non-null   float64
     3   foreign_gross   2037 non-null   object 
     4   year            3387 non-null   int64  
    dtypes: float64(1), int64(1), object(3)
    memory usage: 132.4+ KB
    


```python
bom_df.isnull()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>studio</th>
      <th>domestic_gross</th>
      <th>foreign_gross</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3382</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3383</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3384</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3385</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3386</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>3387 rows × 5 columns</p>
</div>




```python
bom_df.duplicated().sum()
```




    0




```python
#Data processing 
#i will only consider three features here ,foreign gross and domestic gross and title
```


```python
bom_df = bom_df[['studio','title', 'foreign_gross', 'domestic_gross']]

bom_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>studio</th>
      <th>title</th>
      <th>foreign_gross</th>
      <th>domestic_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BV</td>
      <td>Toy Story 3</td>
      <td>652000000</td>
      <td>415000000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BV</td>
      <td>Alice in Wonderland (2010)</td>
      <td>691300000</td>
      <td>334200000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WB</td>
      <td>Harry Potter and the Deathly Hallows Part 1</td>
      <td>664300000</td>
      <td>296000000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>WB</td>
      <td>Inception</td>
      <td>535700000</td>
      <td>292600000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P/DW</td>
      <td>Shrek Forever After</td>
      <td>513900000</td>
      <td>238700000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Remove NaN and non-numeric values from the foreign_gross and domestic_gross columns
bom_df['foreign_gross'] = pd.to_numeric(bom_df['foreign_gross'], errors='coerce')
bom_df['domestic_gross'] = pd.to_numeric(bom_df['domestic_gross'], errors='coerce')
bom_df = bom_df.dropna(subset=['foreign_gross', 'domestic_gross'])
```


```python
import matplotlib.pyplot as plt

plt.scatter(bom_df['foreign_gross'], bom_df['domestic_gross'])
plt.xlabel('Foreign Gross')
plt.ylabel('Domestic Gross')
plt.title('Foreign Gross vs Domestic Gross')
plt.show()

```


    
![png](output_13_0.png)
    


 The scatter plot shows that there is a positive correlation,thus showing that movies with higher domestic gross also has high foreign gross
 



## Data Exploration on zippedData/tmdb.movies.csv.gz


```python
# viewing data on zippedData/tmdb.movies.csv.gz
tm_df = pd.read_csv('zippedData/tmdb.movies.csv.gz')
tm_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>genre_ids</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>popularity</th>
      <th>release_date</th>
      <th>title</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>[12, 14, 10751]</td>
      <td>12444</td>
      <td>en</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>33.533</td>
      <td>2010-11-19</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>7.7</td>
      <td>10788</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>[14, 12, 16, 10751]</td>
      <td>10191</td>
      <td>en</td>
      <td>How to Train Your Dragon</td>
      <td>28.734</td>
      <td>2010-03-26</td>
      <td>How to Train Your Dragon</td>
      <td>7.7</td>
      <td>7610</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>[12, 28, 878]</td>
      <td>10138</td>
      <td>en</td>
      <td>Iron Man 2</td>
      <td>28.515</td>
      <td>2010-05-07</td>
      <td>Iron Man 2</td>
      <td>6.8</td>
      <td>12368</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>[16, 35, 10751]</td>
      <td>862</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>28.005</td>
      <td>1995-11-22</td>
      <td>Toy Story</td>
      <td>7.9</td>
      <td>10174</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>[28, 878, 12]</td>
      <td>27205</td>
      <td>en</td>
      <td>Inception</td>
      <td>27.920</td>
      <td>2010-07-16</td>
      <td>Inception</td>
      <td>8.3</td>
      <td>22186</td>
    </tr>
  </tbody>
</table>
</div>




```python
tm_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 26517 entries, 0 to 26516
    Data columns (total 10 columns):
     #   Column             Non-Null Count  Dtype  
    ---  ------             --------------  -----  
     0   Unnamed: 0         26517 non-null  int64  
     1   genre_ids          26517 non-null  object 
     2   id                 26517 non-null  int64  
     3   original_language  26517 non-null  object 
     4   original_title     26517 non-null  object 
     5   popularity         26517 non-null  float64
     6   release_date       26517 non-null  object 
     7   title              26517 non-null  object 
     8   vote_average       26517 non-null  float64
     9   vote_count         26517 non-null  int64  
    dtypes: float64(2), int64(3), object(5)
    memory usage: 2.0+ MB
    


```python
tm_df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>id</th>
      <th>popularity</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>26517.00000</td>
      <td>26517.000000</td>
      <td>26517.000000</td>
      <td>26517.000000</td>
      <td>26517.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>13258.00000</td>
      <td>295050.153260</td>
      <td>3.130912</td>
      <td>5.991281</td>
      <td>194.224837</td>
    </tr>
    <tr>
      <th>std</th>
      <td>7654.94288</td>
      <td>153661.615648</td>
      <td>4.355229</td>
      <td>1.852946</td>
      <td>960.961095</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.00000</td>
      <td>27.000000</td>
      <td>0.600000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6629.00000</td>
      <td>157851.000000</td>
      <td>0.600000</td>
      <td>5.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>13258.00000</td>
      <td>309581.000000</td>
      <td>1.374000</td>
      <td>6.000000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>19887.00000</td>
      <td>419542.000000</td>
      <td>3.694000</td>
      <td>7.000000</td>
      <td>28.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>26516.00000</td>
      <td>608444.000000</td>
      <td>80.773000</td>
      <td>10.000000</td>
      <td>22186.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
tm_df.isnull()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>genre_ids</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>popularity</th>
      <th>release_date</th>
      <th>title</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>26512</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26513</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26514</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26515</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26516</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>26517 rows × 10 columns</p>
</div>




```python
tm_df.dropna()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>genre_ids</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>popularity</th>
      <th>release_date</th>
      <th>title</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>[12, 14, 10751]</td>
      <td>12444</td>
      <td>en</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>33.533</td>
      <td>2010-11-19</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>7.7</td>
      <td>10788</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>[14, 12, 16, 10751]</td>
      <td>10191</td>
      <td>en</td>
      <td>How to Train Your Dragon</td>
      <td>28.734</td>
      <td>2010-03-26</td>
      <td>How to Train Your Dragon</td>
      <td>7.7</td>
      <td>7610</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>[12, 28, 878]</td>
      <td>10138</td>
      <td>en</td>
      <td>Iron Man 2</td>
      <td>28.515</td>
      <td>2010-05-07</td>
      <td>Iron Man 2</td>
      <td>6.8</td>
      <td>12368</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>[16, 35, 10751]</td>
      <td>862</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>28.005</td>
      <td>1995-11-22</td>
      <td>Toy Story</td>
      <td>7.9</td>
      <td>10174</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>[28, 878, 12]</td>
      <td>27205</td>
      <td>en</td>
      <td>Inception</td>
      <td>27.920</td>
      <td>2010-07-16</td>
      <td>Inception</td>
      <td>8.3</td>
      <td>22186</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>26512</th>
      <td>26512</td>
      <td>[27, 18]</td>
      <td>488143</td>
      <td>en</td>
      <td>Laboratory Conditions</td>
      <td>0.600</td>
      <td>2018-10-13</td>
      <td>Laboratory Conditions</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26513</th>
      <td>26513</td>
      <td>[18, 53]</td>
      <td>485975</td>
      <td>en</td>
      <td>_EXHIBIT_84xxx_</td>
      <td>0.600</td>
      <td>2018-05-01</td>
      <td>_EXHIBIT_84xxx_</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26514</th>
      <td>26514</td>
      <td>[14, 28, 12]</td>
      <td>381231</td>
      <td>en</td>
      <td>The Last One</td>
      <td>0.600</td>
      <td>2018-10-01</td>
      <td>The Last One</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26515</th>
      <td>26515</td>
      <td>[10751, 12, 28]</td>
      <td>366854</td>
      <td>en</td>
      <td>Trailer Made</td>
      <td>0.600</td>
      <td>2018-06-22</td>
      <td>Trailer Made</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26516</th>
      <td>26516</td>
      <td>[53, 27]</td>
      <td>309885</td>
      <td>en</td>
      <td>The Church</td>
      <td>0.600</td>
      <td>2018-10-05</td>
      <td>The Church</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>26517 rows × 10 columns</p>
</div>




```python
tm_df.drop_duplicates()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>genre_ids</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>popularity</th>
      <th>release_date</th>
      <th>title</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>[12, 14, 10751]</td>
      <td>12444</td>
      <td>en</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>33.533</td>
      <td>2010-11-19</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>7.7</td>
      <td>10788</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>[14, 12, 16, 10751]</td>
      <td>10191</td>
      <td>en</td>
      <td>How to Train Your Dragon</td>
      <td>28.734</td>
      <td>2010-03-26</td>
      <td>How to Train Your Dragon</td>
      <td>7.7</td>
      <td>7610</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>[12, 28, 878]</td>
      <td>10138</td>
      <td>en</td>
      <td>Iron Man 2</td>
      <td>28.515</td>
      <td>2010-05-07</td>
      <td>Iron Man 2</td>
      <td>6.8</td>
      <td>12368</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>[16, 35, 10751]</td>
      <td>862</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>28.005</td>
      <td>1995-11-22</td>
      <td>Toy Story</td>
      <td>7.9</td>
      <td>10174</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>[28, 878, 12]</td>
      <td>27205</td>
      <td>en</td>
      <td>Inception</td>
      <td>27.920</td>
      <td>2010-07-16</td>
      <td>Inception</td>
      <td>8.3</td>
      <td>22186</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>26512</th>
      <td>26512</td>
      <td>[27, 18]</td>
      <td>488143</td>
      <td>en</td>
      <td>Laboratory Conditions</td>
      <td>0.600</td>
      <td>2018-10-13</td>
      <td>Laboratory Conditions</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26513</th>
      <td>26513</td>
      <td>[18, 53]</td>
      <td>485975</td>
      <td>en</td>
      <td>_EXHIBIT_84xxx_</td>
      <td>0.600</td>
      <td>2018-05-01</td>
      <td>_EXHIBIT_84xxx_</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26514</th>
      <td>26514</td>
      <td>[14, 28, 12]</td>
      <td>381231</td>
      <td>en</td>
      <td>The Last One</td>
      <td>0.600</td>
      <td>2018-10-01</td>
      <td>The Last One</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26515</th>
      <td>26515</td>
      <td>[10751, 12, 28]</td>
      <td>366854</td>
      <td>en</td>
      <td>Trailer Made</td>
      <td>0.600</td>
      <td>2018-06-22</td>
      <td>Trailer Made</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26516</th>
      <td>26516</td>
      <td>[53, 27]</td>
      <td>309885</td>
      <td>en</td>
      <td>The Church</td>
      <td>0.600</td>
      <td>2018-10-05</td>
      <td>The Church</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>26517 rows × 10 columns</p>
</div>




```python
tm_df.value_counts()
```




    Unnamed: 0  genre_ids            id      original_language  original_title                                popularity  release_date  title                                         vote_average  vote_count
    0           [12, 14, 10751]      12444   en                 Harry Potter and the Deathly Hallows: Part 1  33.533      2010-11-19    Harry Potter and the Deathly Hallows: Part 1  7.7           10788         1
    17675       [18, 27]             340103  en                 The Monster                                   8.515       2016-11-11    The Monster                                   5.2           242           1
    17685       [37, 18]             333386  en                 The Duel                                      8.433       2016-06-24    The Duel                                      5.4           150           1
    17684       [18, 10749, 10770]   410314  en                 A Wish for Christmas                          8.437       2016-11-05    A Wish for Christmas                          6.1           125           1
    17683       [28, 12, 16, 10751]  234004  en                 Ratchet & Clank                               8.439       2016-04-29    Ratchet & Clank                               5.5           332           1
                                                                                                                                                                                                                 ..
    8836        [18, 10749]          142115  en                 Five Dances                                   2.230       2013-10-04    Five Dances                                   6.9           32            1
    8835        [53]                 248694  en                 Truth                                         2.232       2013-07-12    Truth                                         5.9           13            1
    8834        [35, 12]             120802  en                 Noobz                                         2.232       2013-01-25    Noobz                                         6.0           23            1
    8833        [35, 18]             203780  ru                 Igra v Pravdu                                 2.235       2013-07-07    The Game of Truth                             6.2           11            1
    26516       [53, 27]             309885  en                 The Church                                    0.600       2018-10-05    The Church                                    0.0           1             1
    Length: 26517, dtype: int64




```python
# loading and viewing data
tn_movies=pd.read_csv("zippedData/tn.movie_budgets.csv.gz", index_col=0)
tn_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
    </tr>
    <tr>
      <th>2</th>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$410,600,000</td>
      <td>$241,063,875</td>
      <td>$1,045,663,875</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>$350,000,000</td>
      <td>$42,762,350</td>
      <td>$149,762,350</td>
    </tr>
    <tr>
      <th>4</th>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>$330,600,000</td>
      <td>$459,005,868</td>
      <td>$1,403,013,963</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dec 15, 2017</td>
      <td>Star Wars Ep. VIII: The Last Jedi</td>
      <td>$317,000,000</td>
      <td>$620,181,382</td>
      <td>$1,316,721,747</td>
    </tr>
  </tbody>
</table>
</div>




```python
tn_movies.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5782</td>
      <td>5782</td>
      <td>5782</td>
      <td>5782</td>
      <td>5782</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>2418</td>
      <td>5698</td>
      <td>509</td>
      <td>5164</td>
      <td>5356</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Dec 31, 2014</td>
      <td>Halloween</td>
      <td>$20,000,000</td>
      <td>$0</td>
      <td>$0</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>24</td>
      <td>3</td>
      <td>231</td>
      <td>548</td>
      <td>367</td>
    </tr>
  </tbody>
</table>
</div>




```python
tn_movies.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 5782 entries, 1 to 82
    Data columns (total 5 columns):
     #   Column             Non-Null Count  Dtype 
    ---  ------             --------------  ----- 
     0   release_date       5782 non-null   object
     1   movie              5782 non-null   object
     2   production_budget  5782 non-null   object
     3   domestic_gross     5782 non-null   object
     4   worldwide_gross    5782 non-null   object
    dtypes: object(5)
    memory usage: 271.0+ KB
    


```python
print(tn_movies.isna().sum().sum())
```

    0
    


```python
# loading and viewing zippedData/rt.movie_info.tsv.gz dataset
rt_movies = pd.read_csv('zippedData/rt.movie_info.tsv.gz',sep='\t')
rt_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>synopsis</th>
      <th>rating</th>
      <th>genre</th>
      <th>director</th>
      <th>writer</th>
      <th>theater_date</th>
      <th>dvd_date</th>
      <th>currency</th>
      <th>box_office</th>
      <th>runtime</th>
      <th>studio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>New York City, not-too-distant-future: Eric Pa...</td>
      <td>R</td>
      <td>Drama|Science Fiction and Fantasy</td>
      <td>David Cronenberg</td>
      <td>David Cronenberg|Don DeLillo</td>
      <td>Aug 17, 2012</td>
      <td>Jan 1, 2013</td>
      <td>$</td>
      <td>600,000</td>
      <td>108 minutes</td>
      <td>Entertainment One</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>Illeana Douglas delivers a superb performance ...</td>
      <td>R</td>
      <td>Drama|Musical and Performing Arts</td>
      <td>Allison Anders</td>
      <td>Allison Anders</td>
      <td>Sep 13, 1996</td>
      <td>Apr 18, 2000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>116 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>Michael Douglas runs afoul of a treacherous su...</td>
      <td>R</td>
      <td>Drama|Mystery and Suspense</td>
      <td>Barry Levinson</td>
      <td>Paul Attanasio|Michael Crichton</td>
      <td>Dec 9, 1994</td>
      <td>Aug 27, 1997</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>NaN</td>
      <td>NR</td>
      <td>Drama|Romance</td>
      <td>Rodney Bennett</td>
      <td>Giles Cooper</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>200 minutes</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
rt_movies.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1560.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1007.303846</td>
    </tr>
    <tr>
      <th>std</th>
      <td>579.164527</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>504.750000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1007.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1503.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2000.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
rt_movies.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1560 entries, 0 to 1559
    Data columns (total 12 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   id            1560 non-null   int64 
     1   synopsis      1498 non-null   object
     2   rating        1557 non-null   object
     3   genre         1552 non-null   object
     4   director      1361 non-null   object
     5   writer        1111 non-null   object
     6   theater_date  1201 non-null   object
     7   dvd_date      1201 non-null   object
     8   currency      340 non-null    object
     9   box_office    340 non-null    object
     10  runtime       1530 non-null   object
     11  studio        494 non-null    object
    dtypes: int64(1), object(11)
    memory usage: 146.4+ KB
    

# DATA ANALYSIS AND  CLEANING FOR THE FOUR CHOSEN DATASETS


```python
# cleaning and chosing the data to use in final analysis
#bom_df = pd.read_csv('zippedData/bom.movie_gross.csv.gz')
# i chose to work with the below columns on the bom_df dataset
bom_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>studio</th>
      <th>title</th>
      <th>foreign_gross</th>
      <th>domestic_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BV</td>
      <td>Toy Story 3</td>
      <td>652000000.0</td>
      <td>415000000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BV</td>
      <td>Alice in Wonderland (2010)</td>
      <td>691300000.0</td>
      <td>334200000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WB</td>
      <td>Harry Potter and the Deathly Hallows Part 1</td>
      <td>664300000.0</td>
      <td>296000000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>WB</td>
      <td>Inception</td>
      <td>535700000.0</td>
      <td>292600000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>P/DW</td>
      <td>Shrek Forever After</td>
      <td>513900000.0</td>
      <td>238700000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt

# Get top 10 movies by domestic gross revenue
top_10 = bom_df.sort_values(by='domestic_gross', ascending=False).head(10)

# Create bar plot
plt.bar(top_10['title'], top_10['domestic_gross'])

# Rotate x-axis labels for readability
plt.xticks(rotation=90)

# Add axis labels and title
plt.xlabel('Movie Title')
plt.ylabel('Domestic and  Box Office Revenue (in millions)')
plt.title('Top 10 Movies by Domestic Gross Box Office Revenue')

# Show plot
plt.show()

```


    
![png](output_32_0.png)
    



```python
# converting string integr and then get descriptive statistics
a = bom_df['foreign_gross'].dropna().reset_index()
a['foreign_gross'] = pd.to_numeric(a['foreign_gross'], errors='coerce')
a['foreign_gross'].describe()
```




    count    2.004000e+03
    mean     7.590713e+07
    std      1.382501e+08
    min      6.000000e+02
    25%      3.900000e+06
    50%      1.955000e+07
    75%      7.615000e+07
    max      9.605000e+08
    Name: foreign_gross, dtype: float64




```python
# ploting a bar graph on top studos doing well
bom_df_studio = bom_df['studio'].value_counts().head(10)
bom_df_studio
# plotting studio 
bom_df['studio'].value_counts().head(10).plot(kind = 'bar')
plt.title('Top Ten Movie Studios')
```




    Text(0.5, 1.0, 'Top Ten Movie Studios')




    
![png](output_34_1.png)
    



```python
rt_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>synopsis</th>
      <th>rating</th>
      <th>genre</th>
      <th>director</th>
      <th>writer</th>
      <th>theater_date</th>
      <th>dvd_date</th>
      <th>currency</th>
      <th>box_office</th>
      <th>runtime</th>
      <th>studio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>New York City, not-too-distant-future: Eric Pa...</td>
      <td>R</td>
      <td>Drama|Science Fiction and Fantasy</td>
      <td>David Cronenberg</td>
      <td>David Cronenberg|Don DeLillo</td>
      <td>Aug 17, 2012</td>
      <td>Jan 1, 2013</td>
      <td>$</td>
      <td>600,000</td>
      <td>108 minutes</td>
      <td>Entertainment One</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>Illeana Douglas delivers a superb performance ...</td>
      <td>R</td>
      <td>Drama|Musical and Performing Arts</td>
      <td>Allison Anders</td>
      <td>Allison Anders</td>
      <td>Sep 13, 1996</td>
      <td>Apr 18, 2000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>116 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>Michael Douglas runs afoul of a treacherous su...</td>
      <td>R</td>
      <td>Drama|Mystery and Suspense</td>
      <td>Barry Levinson</td>
      <td>Paul Attanasio|Michael Crichton</td>
      <td>Dec 9, 1994</td>
      <td>Aug 27, 1997</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128 minutes</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>NaN</td>
      <td>NR</td>
      <td>Drama|Romance</td>
      <td>Rodney Bennett</td>
      <td>Giles Cooper</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>200 minutes</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# checking and viewing best movie studios
rt_movies['studio'].value_counts().head(10).plot(kind = 'bar')
plt.title('Top Ten Movie Studios')
```




    Text(0.5, 1.0, 'Top Ten Movie Studios')




    
![png](output_36_1.png)
    



```python
# set figure size
# viewing top 25 genres that are doing well
plt.figure(figsize=(12, 8))

# plot bar chart
rt_movies['genre'].value_counts().head(25).plot(kind='bar')

# set x and y labels and title
plt.xlabel('Genres')
plt.ylabel('Count')
plt.title('Top 25 Genres in Rotten tomatoes Review Dataset')

# show the plot
plt.show()
```


    
![png](output_37_0.png)
    



```python
import pandas as pd

# Load the datasets
rt_movies = pd.read_csv('zippedData/rt.movie_info.tsv.gz', sep='\t')
bom_df = pd.read_csv('zippedData/bom.movie_gross.csv.gz')

# Merge the datasets based on the 'studio' column
merged_df = pd.merge(rt_movies, bom_df, on='studio')

# View the first few rows of the merged dataset
merged_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>synopsis</th>
      <th>rating</th>
      <th>genre</th>
      <th>director</th>
      <th>writer</th>
      <th>theater_date</th>
      <th>dvd_date</th>
      <th>currency</th>
      <th>box_office</th>
      <th>runtime</th>
      <th>studio</th>
      <th>title</th>
      <th>domestic_gross</th>
      <th>foreign_gross</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>Outside the Law (Hors-la-loi)</td>
      <td>96900.0</td>
      <td>3300000</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>Fireflies in the Garden</td>
      <td>70600.0</td>
      <td>3300000</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>Keith Lemon: The Film</td>
      <td>NaN</td>
      <td>4000000</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>Plot for Peace</td>
      <td>7100.0</td>
      <td>NaN</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>Secret Superstar</td>
      <td>NaN</td>
      <td>122000000</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the merged dataset
merged_df = pd.merge(pd.read_csv('zippedData/rt.movie_info.tsv.gz', sep='\t'), pd.read_csv('zippedData/bom.movie_gross.csv.gz'))

# Remove any unnecessary columns
merged_df.drop(['id', 'synopsis', 'rating', 'director', 'writer', 'theater_date', 'currency', 'foreign_gross'], axis=1, inplace=True)

# Remove any rows with missing data
merged_df.dropna(inplace=True)

# Convert year column to datetime format
merged_df['year'] = pd.to_datetime(merged_df['year'], format='%Y')

# Extract year from the datetime column
merged_df['year'] = merged_df['year'].dt.year

# Group data by genre and year and calculate the count of movies in each group
grouped_df = merged_df.groupby(['genre', 'year'])['title'].count().reset_index()

# Create pivot table of movie counts by year and genre
pivot_df = grouped_df.pivot_table(index='year', columns='genre', values='title')

# Plot a bar graph of the pivot table
ax = pivot_df.plot(kind='bar', figsize=(15, 8), width=0.8, fontsize=12)
ax.set_title('Number of Movies by Genre and Year', fontsize=18)
ax.set_xlabel('Year', fontsize=14)
ax.set_ylabel('Number of Movies', fontsize=14)
plt.show()
```


    
![png](output_39_0.png)
    



```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the datasets and merge them as shown in the previous example
rt_movies = pd.read_csv('zippedData/rt.movie_info.tsv.gz', sep='\t')
bom_df = pd.read_csv('zippedData/bom.movie_gross.csv.gz')
merged_df = pd.merge(rt_movies, bom_df, on='studio')

# Group the merged dataset by genre and studio, and count the number of movies in each group
grouped_df = merged_df.groupby(['genre', 'studio']).size().reset_index(name='count')

# Create a bar graph of genre vs studio using the grouped data
grouped_df.plot(kind='bar', x='genre', y='count', figsize=(12,8))
plt.title('Number of Movies by Genre and Studio')
plt.xlabel('Genre')
plt.ylabel('Number of Movies')
plt.show()
```


    
![png](output_40_0.png)
    



```python
tn_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
    </tr>
    <tr>
      <th>2</th>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$410,600,000</td>
      <td>$241,063,875</td>
      <td>$1,045,663,875</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>$350,000,000</td>
      <td>$42,762,350</td>
      <td>$149,762,350</td>
    </tr>
    <tr>
      <th>4</th>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>$330,600,000</td>
      <td>$459,005,868</td>
      <td>$1,403,013,963</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dec 15, 2017</td>
      <td>Star Wars Ep. VIII: The Last Jedi</td>
      <td>$317,000,000</td>
      <td>$620,181,382</td>
      <td>$1,316,721,747</td>
    </tr>
  </tbody>
</table>
</div>




```python
bom_df = pd.read_csv("zippedData/bom.movie_gross.csv.gz")
tn_movies = pd.read_csv("zippedData/tn.movie_budgets.csv.gz")
merged_df = pd.merge(bom_df, tn_movies, left_on='title', right_on='movie', how='inner')
merged_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>studio</th>
      <th>domestic_gross_x</th>
      <th>foreign_gross</th>
      <th>year</th>
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross_y</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Toy Story 3</td>
      <td>BV</td>
      <td>415000000.0</td>
      <td>652000000</td>
      <td>2010</td>
      <td>47</td>
      <td>Jun 18, 2010</td>
      <td>Toy Story 3</td>
      <td>$200,000,000</td>
      <td>$415,004,880</td>
      <td>$1,068,879,522</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Inception</td>
      <td>WB</td>
      <td>292600000.0</td>
      <td>535700000</td>
      <td>2010</td>
      <td>38</td>
      <td>Jul 16, 2010</td>
      <td>Inception</td>
      <td>$160,000,000</td>
      <td>$292,576,195</td>
      <td>$835,524,642</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shrek Forever After</td>
      <td>P/DW</td>
      <td>238700000.0</td>
      <td>513900000</td>
      <td>2010</td>
      <td>27</td>
      <td>May 21, 2010</td>
      <td>Shrek Forever After</td>
      <td>$165,000,000</td>
      <td>$238,736,787</td>
      <td>$756,244,673</td>
    </tr>
    <tr>
      <th>3</th>
      <td>The Twilight Saga: Eclipse</td>
      <td>Sum.</td>
      <td>300500000.0</td>
      <td>398000000</td>
      <td>2010</td>
      <td>53</td>
      <td>Jun 30, 2010</td>
      <td>The Twilight Saga: Eclipse</td>
      <td>$68,000,000</td>
      <td>$300,531,751</td>
      <td>$706,102,828</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Iron Man 2</td>
      <td>Par.</td>
      <td>312400000.0</td>
      <td>311500000</td>
      <td>2010</td>
      <td>15</td>
      <td>May 7, 2010</td>
      <td>Iron Man 2</td>
      <td>$170,000,000</td>
      <td>$312,433,331</td>
      <td>$621,156,389</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1242</th>
      <td>Gotti</td>
      <td>VE</td>
      <td>4300000.0</td>
      <td>NaN</td>
      <td>2018</td>
      <td>64</td>
      <td>Jun 15, 2018</td>
      <td>Gotti</td>
      <td>$10,000,000</td>
      <td>$4,286,367</td>
      <td>$6,089,100</td>
    </tr>
    <tr>
      <th>1243</th>
      <td>Ben is Back</td>
      <td>RAtt.</td>
      <td>3700000.0</td>
      <td>NaN</td>
      <td>2018</td>
      <td>95</td>
      <td>Dec 7, 2018</td>
      <td>Ben is Back</td>
      <td>$13,000,000</td>
      <td>$3,703,182</td>
      <td>$9,633,111</td>
    </tr>
    <tr>
      <th>1244</th>
      <td>Bilal: A New Breed of Hero</td>
      <td>VE</td>
      <td>491000.0</td>
      <td>1700000</td>
      <td>2018</td>
      <td>100</td>
      <td>Feb 2, 2018</td>
      <td>Bilal: A New Breed of Hero</td>
      <td>$30,000,000</td>
      <td>$490,973</td>
      <td>$648,599</td>
    </tr>
    <tr>
      <th>1245</th>
      <td>Mandy</td>
      <td>RLJ</td>
      <td>1200000.0</td>
      <td>NaN</td>
      <td>2018</td>
      <td>71</td>
      <td>Sep 14, 2018</td>
      <td>Mandy</td>
      <td>$6,000,000</td>
      <td>$1,214,525</td>
      <td>$1,427,656</td>
    </tr>
    <tr>
      <th>1246</th>
      <td>Lean on Pete</td>
      <td>A24</td>
      <td>1200000.0</td>
      <td>NaN</td>
      <td>2018</td>
      <td>13</td>
      <td>Apr 6, 2018</td>
      <td>Lean on Pete</td>
      <td>$8,000,000</td>
      <td>$1,163,056</td>
      <td>$2,455,027</td>
    </tr>
  </tbody>
</table>
<p>1247 rows × 11 columns</p>
</div>




```python
# removing $ to make it workable
merged_df['worldwide_gross'] = merged_df['worldwide_gross'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
merged_df['production_budget'] = merged_df['production_budget'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)

```

    C:\Users\pc\AppData\Local\Temp\ipykernel_16028\1524873247.py:1: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will *not* be treated as literal strings when regex=True.
      merged_df['worldwide_gross'] = merged_df['worldwide_gross'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
    C:\Users\pc\AppData\Local\Temp\ipykernel_16028\1524873247.py:2: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will *not* be treated as literal strings when regex=True.
      merged_df['production_budget'] = merged_df['production_budget'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
    


```python
# the merged tn_movies and bom_movies datasets for better analysis
merged_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>studio</th>
      <th>domestic_gross_x</th>
      <th>foreign_gross</th>
      <th>year</th>
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross_y</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Toy Story 3</td>
      <td>BV</td>
      <td>415000000.0</td>
      <td>652000000</td>
      <td>2010</td>
      <td>47</td>
      <td>Jun 18, 2010</td>
      <td>Toy Story 3</td>
      <td>200000000.0</td>
      <td>$415,004,880</td>
      <td>1.068880e+09</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Inception</td>
      <td>WB</td>
      <td>292600000.0</td>
      <td>535700000</td>
      <td>2010</td>
      <td>38</td>
      <td>Jul 16, 2010</td>
      <td>Inception</td>
      <td>160000000.0</td>
      <td>$292,576,195</td>
      <td>8.355246e+08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shrek Forever After</td>
      <td>P/DW</td>
      <td>238700000.0</td>
      <td>513900000</td>
      <td>2010</td>
      <td>27</td>
      <td>May 21, 2010</td>
      <td>Shrek Forever After</td>
      <td>165000000.0</td>
      <td>$238,736,787</td>
      <td>7.562447e+08</td>
    </tr>
    <tr>
      <th>3</th>
      <td>The Twilight Saga: Eclipse</td>
      <td>Sum.</td>
      <td>300500000.0</td>
      <td>398000000</td>
      <td>2010</td>
      <td>53</td>
      <td>Jun 30, 2010</td>
      <td>The Twilight Saga: Eclipse</td>
      <td>68000000.0</td>
      <td>$300,531,751</td>
      <td>7.061028e+08</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Iron Man 2</td>
      <td>Par.</td>
      <td>312400000.0</td>
      <td>311500000</td>
      <td>2010</td>
      <td>15</td>
      <td>May 7, 2010</td>
      <td>Iron Man 2</td>
      <td>170000000.0</td>
      <td>$312,433,331</td>
      <td>6.211564e+08</td>
    </tr>
  </tbody>
</table>
</div>




```python

# Calculate ROI and create top 10 dataframe
merged_df['worldwide_gross'] = merged_df['worldwide_gross'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
merged_df['production_budget'] = merged_df['production_budget'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
merged_df['roi'] = (merged_df['worldwide_gross'] - merged_df['production_budget']) / merged_df['production_budget'] * 100
top_10 = merged_df.sort_values('roi', ascending=False).head(10)

# Create bar plot
sns.barplot(x='title', y='roi', data=top_10)
plt.xticks(rotation=90)
plt.ylabel('ROI (%)')
plt.title('Top 10 Movies by ROI')
plt.show()
```

    C:\Users\pc\AppData\Local\Temp\ipykernel_16028\1222537528.py:2: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will *not* be treated as literal strings when regex=True.
      merged_df['worldwide_gross'] = merged_df['worldwide_gross'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
    C:\Users\pc\AppData\Local\Temp\ipykernel_16028\1222537528.py:3: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will *not* be treated as literal strings when regex=True.
      merged_df['production_budget'] = merged_df['production_budget'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
    


    
![png](output_45_1.png)
    



```python
tm_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>genre_ids</th>
      <th>id</th>
      <th>original_language</th>
      <th>original_title</th>
      <th>popularity</th>
      <th>release_date</th>
      <th>title</th>
      <th>vote_average</th>
      <th>vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>[12, 14, 10751]</td>
      <td>12444</td>
      <td>en</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>33.533</td>
      <td>2010-11-19</td>
      <td>Harry Potter and the Deathly Hallows: Part 1</td>
      <td>7.7</td>
      <td>10788</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>[14, 12, 16, 10751]</td>
      <td>10191</td>
      <td>en</td>
      <td>How to Train Your Dragon</td>
      <td>28.734</td>
      <td>2010-03-26</td>
      <td>How to Train Your Dragon</td>
      <td>7.7</td>
      <td>7610</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>[12, 28, 878]</td>
      <td>10138</td>
      <td>en</td>
      <td>Iron Man 2</td>
      <td>28.515</td>
      <td>2010-05-07</td>
      <td>Iron Man 2</td>
      <td>6.8</td>
      <td>12368</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>[16, 35, 10751]</td>
      <td>862</td>
      <td>en</td>
      <td>Toy Story</td>
      <td>28.005</td>
      <td>1995-11-22</td>
      <td>Toy Story</td>
      <td>7.9</td>
      <td>10174</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>[28, 878, 12]</td>
      <td>27205</td>
      <td>en</td>
      <td>Inception</td>
      <td>27.920</td>
      <td>2010-07-16</td>
      <td>Inception</td>
      <td>8.3</td>
      <td>22186</td>
    </tr>
  </tbody>
</table>
</div>




```python

# Create a data frame
data = {
    'title': ['Harry Potter and the Deathly Hallows: Part 1', 'How to Train Your Dragon', 'Iron Man 2', 'Toy Story', 'Inception'],
    'vote_average': [7.7, 7.7, 6.8, 7.9, 8.3]
}
df = pd.DataFrame(data)

# Create a bar plot
df.plot(kind='bar', x='title', y='vote_average')

# Set the plot title and axis labels
plt.title('Movie Ratings')
plt.xlabel('Title')
plt.ylabel('Vote Average')

# Show the plot
plt.show()

```


    
![png](output_47_0.png)
    



```python
tn_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Dec 18, 2009</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>May 20, 2011</td>
      <td>Pirates of the Caribbean: On Stranger Tides</td>
      <td>$410,600,000</td>
      <td>$241,063,875</td>
      <td>$1,045,663,875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Jun 7, 2019</td>
      <td>Dark Phoenix</td>
      <td>$350,000,000</td>
      <td>$42,762,350</td>
      <td>$149,762,350</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>May 1, 2015</td>
      <td>Avengers: Age of Ultron</td>
      <td>$330,600,000</td>
      <td>$459,005,868</td>
      <td>$1,403,013,963</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Dec 15, 2017</td>
      <td>Star Wars Ep. VIII: The Last Jedi</td>
      <td>$317,000,000</td>
      <td>$620,181,382</td>
      <td>$1,316,721,747</td>
    </tr>
  </tbody>
</table>
</div>




```python
# convert release date column to datetime values
tn_movies['release_date'] = pd.to_datetime(tn_movies['release_date'])
# am creating release month column
tn_movies['release_month'] = tn_movies['release_date'].dt.strftime('%B')
# plotting a  graph for the release month
tn_movies['release_month'].value_counts().plot(kind='bar')
plt.title('Release Month')

```




    Text(0.5, 1.0, 'Release Month')




    
![png](output_49_1.png)
    



```python
# working on the merged datasets rt_movies and tn_movies to achieve ROI
merged_movies = pd.merge(rt_movies, tn_movies, on='id', how='inner')
merged_movies.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>synopsis</th>
      <th>rating</th>
      <th>genre</th>
      <th>director</th>
      <th>writer</th>
      <th>theater_date</th>
      <th>dvd_date</th>
      <th>currency</th>
      <th>box_office</th>
      <th>runtime</th>
      <th>studio</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>release_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2009-12-18</td>
      <td>Avatar</td>
      <td>$425,000,000</td>
      <td>$760,507,625</td>
      <td>$2,776,345,279</td>
      <td>December</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2009-05-29</td>
      <td>Up</td>
      <td>$175,000,000</td>
      <td>$293,004,164</td>
      <td>$731,463,377</td>
      <td>May</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2014-03-07</td>
      <td>Mr. Peabody &amp; Sherman</td>
      <td>$145,000,000</td>
      <td>$111,506,430</td>
      <td>$269,806,430</td>
      <td>March</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2010-12-17</td>
      <td>How Do You Know?</td>
      <td>$120,000,000</td>
      <td>$30,212,620</td>
      <td>$49,628,177</td>
      <td>December</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2015-12-11</td>
      <td>In the Heart of the Sea</td>
      <td>$100,000,000</td>
      <td>$25,020,758</td>
      <td>$89,693,309</td>
      <td>December</td>
    </tr>
  </tbody>
</table>
</div>




```python
merged_movies['worldwide_gross'] = merged_movies['worldwide_gross'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
merged_movies['production_budget'] = merged_movies['production_budget'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)

```

    C:\Users\pc\AppData\Local\Temp\ipykernel_16028\2917971715.py:1: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will *not* be treated as literal strings when regex=True.
      merged_movies['worldwide_gross'] = merged_movies['worldwide_gross'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
    C:\Users\pc\AppData\Local\Temp\ipykernel_16028\2917971715.py:2: FutureWarning: The default value of regex will change from True to False in a future version. In addition, single character regular expressions will *not* be treated as literal strings when regex=True.
      merged_movies['production_budget'] = merged_movies['production_budget'].astype(str).str.replace(',', '').str.replace('$', '').astype(float)
    


```python
merged_movies['worldwide_gross'] = merged_movies['worldwide_gross'].astype(str).str.replace(',', '', regex=False).str.replace('$', '', regex=False).astype(float)
merged_movies['production_budget'] = merged_movies['production_budget'].astype(str).str.replace(',', '', regex=False).str.replace('$', '', regex=False).astype(float)

```


```python
merged_movies.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>synopsis</th>
      <th>rating</th>
      <th>genre</th>
      <th>director</th>
      <th>writer</th>
      <th>theater_date</th>
      <th>dvd_date</th>
      <th>currency</th>
      <th>box_office</th>
      <th>runtime</th>
      <th>studio</th>
      <th>release_date</th>
      <th>movie</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>release_month</th>
      <th>roi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2009-12-18</td>
      <td>Avatar</td>
      <td>425000000.0</td>
      <td>$760,507,625</td>
      <td>2.776345e+09</td>
      <td>December</td>
      <td>5.532577</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2009-05-29</td>
      <td>Up</td>
      <td>175000000.0</td>
      <td>$293,004,164</td>
      <td>7.314634e+08</td>
      <td>May</td>
      <td>3.179791</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2014-03-07</td>
      <td>Mr. Peabody &amp; Sherman</td>
      <td>145000000.0</td>
      <td>$111,506,430</td>
      <td>2.698064e+08</td>
      <td>March</td>
      <td>0.860734</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2010-12-17</td>
      <td>How Do You Know?</td>
      <td>120000000.0</td>
      <td>$30,212,620</td>
      <td>4.962818e+07</td>
      <td>December</td>
      <td>-0.586432</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2015-12-11</td>
      <td>In the Heart of the Sea</td>
      <td>100000000.0</td>
      <td>$25,020,758</td>
      <td>8.969331e+07</td>
      <td>December</td>
      <td>-0.103067</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2007-06-08</td>
      <td>Ocean's Thirteen</td>
      <td>85000000.0</td>
      <td>$117,144,465</td>
      <td>3.117445e+08</td>
      <td>June</td>
      <td>2.667582</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2003-11-26</td>
      <td>Timeline</td>
      <td>80000000.0</td>
      <td>$19,480,739</td>
      <td>2.670318e+07</td>
      <td>November</td>
      <td>-0.666210</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2009-08-21</td>
      <td>Inglourious Basterds</td>
      <td>70000000.0</td>
      <td>$120,774,594</td>
      <td>3.169153e+08</td>
      <td>August</td>
      <td>3.527361</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>2012-11-21</td>
      <td>Red Dawn</td>
      <td>65000000.0</td>
      <td>$44,806,783</td>
      <td>4.816415e+07</td>
      <td>November</td>
      <td>-0.259013</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>This gritty, fast-paced, and innovative police...</td>
      <td>R</td>
      <td>Action and Adventure|Classics|Drama</td>
      <td>William Friedkin</td>
      <td>Ernest Tidyman</td>
      <td>Oct 9, 1971</td>
      <td>Sep 25, 2001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>104 minutes</td>
      <td>NaN</td>
      <td>1997-11-26</td>
      <td>Alien: Resurrection</td>
      <td>60000000.0</td>
      <td>$47,795,018</td>
      <td>1.607000e+08</td>
      <td>November</td>
      <td>1.678333</td>
    </tr>
  </tbody>
</table>
</div>




```python
#plot ROI on genres to see the correlation 
merged_movies['roi'] = (merged_movies['worldwide_gross'] - merged_movies['production_budget']) / merged_movies['production_budget']

# group movies by genre and calculate mean ROI for each genre
roi_by_genre = merged_movies.groupby('genre')['roi'].mean().sort_values()

# create bar graph of mean ROI vs genre
plt.bar(roi_by_genre.index, roi_by_genre.values)

# set title and axis labels
plt.title('Mean ROI by Genre')
plt.xlabel('Genre')
plt.xticks(rotation=90, fontsize=8)
plt.ylabel('Mean ROI',fontsize=10)

# display the plot
plt.show()
```


    
![png](output_54_0.png)
    



```python

```
