# Manipulate Time Data

![](https://media.giphy.com/media/d3yxg15kJppJilnW/giphy.gif)

**This morning** we will practice loading in and manipulating time series data.

In the cell below we import a dataset that counts the number of monthly [sunspots](https://en.wikipedia.org/wiki/Sunspot#:~:text=Sunspots%20are%20temporary%20phenomena%20on,pairs%20of%20opposite%20magnetic%20polarity.) from 1749-2019


```python
import pandas as pd
import matplotlib.pyplot as plt
from test_scripts.test_class import Test
test = Test()

df = pd.read_csv('data/Sunspots.csv')
df = df.iloc[:,1:]
df.columns  = ['date', 'sunspots']
df.head()
```

Let's check the datatype for the `date` column.


```python
df.date.dtype
```

Currently, the `date` column is an `Object` datatype which is the datatype pandas used for strings.

<u><b>In the cell below:</b></u>
1. Change the datatype of the `date` column to `datetime`.
2. Set the `date` column as the index for the `df` variable.


```python
# Your code here

```

Run the cell below to test your results!


```python
test.run_test(df, 'sunspot_date_index')
```

Ok, let's take a look at the sunspots data.

<u><b>In the cell below</b></u>, plot a simple line plot of the sunspots column, using the datetime index as the x-axis


```python
df.sunspots.plot(figsize=(15,4));
```

Please describe the data. Do you see any trends or Seasonality?


```python
# Your answer here

```

**Let's find the rolling mean with a window of 3 time steps**


```python
# Find the rolling mean with the .rolling method
rolling_mean = df.sunspots.rolling(window=3).mean()

# Plot the rolling mean and the original data together
plt.figure(figsize=(15,4))
plt.plot(df.index, df.sunspots, label='Series')
plt.plot(df.index, rolling_mean, label='Rolling Mean')
plt.legend();
```

**Ok Ok,** Let's define a function called `rolling_mean_diff` that, when given a series and a window size:
1. Will find the rolling mean with the provided window size
2. Subtract the rolling mean from the original series. 
3. Return the differenced time series


```python
# Your code here
```

Now,  let's use our `rolling_mean_diff` function to see if subtracting the rolling mean results in a stationary time series.


```python
sunspots_rolling_mean_diff = rolling_mean_diff(df.sunspots)
```

Run the cell below to test your results!


```python
test.run_test(sunspots_rolling_mean_diff, 'sunspots_rolling_mean_diff')
```

Now, let's plot the newly differenced time series.


```python
sunspots_rolling_mean_diff.plot(figsize=(15,4));
```

Please interpret the graph above. Is it stationary?


```python
# Your answer here

```

## Resample

Lastly, let's resample our data.

We will down sample our data to a `calendar year end` [yearly frequency](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#dateoffset-objects).



```python
yearly = df.sunspots.resample('A').mean()
```

Run the cell below to test your results!


```python
test.run_test(yearly, 'yearly_resample')
```

Let's take a look at our yearly time series.


```python
yearly.plot(figsize=(15,4), title='Resampled Yearly');
```
