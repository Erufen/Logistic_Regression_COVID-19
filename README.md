# Logistic Regression with dataset of COVID-19 

The aim of the projets is to predict the number of deaths that COVID-19 will cause.

Unfortunately, several waves will (certainly) follow one another.


## Current number of deaths in the countries studied

Italy, Spain, UK and France


 ````
 total = df.drop(['Province/State', 'Lat', 'Long'], 
        axis=1).groupby('Country/Region').sum().max(axis=1).sort_values(ascending=False)
countries = total.index.to_list()
deaths = pd.DataFrame()

for country in countries:
    temp = df[df['Country/Region'] == country][df.columns[4:]].T.sum(axis=1)
    temp.index = pd.to_datetime(temp.index)
    temp = temp.to_frame(country)
    deaths = pd.concat([deaths, temp], axis=1)
    
start = '2020-09' # to change the date
ax = deaths[['Italy', 'Spain', 'United Kingdom', 'France']][start:].plot(style='-', figsize=FS) # to change the country
markers = itertools.cycle(("o", "v", "^", "<", ">", "s", "p",
                           "P", "*", "h", "X", "D", '.')) # style 

for i, line in enumerate(ax.get_lines()):
    marker = next(markers)
    line.set_marker(marker)
    
_ = ax.legend()
_ = ax.set_title("Number of COVID-19 deaths per country")
 
 ````
 
 ![Zozor](https://zupimages.net/up/21/04/uf5z.png)
 
 
 ## Functions used to build the logistic curve
 
 1. ratios
 
 ````
 def plot_ratios(country, death_min=0, death_max=None):
    """ Plot the proportional growth rate with respect to D, 
        on the interval (death_min, death_max).
    """
    country = country[country > death_min]
    
    if death_max is not None:
        country = country[country < death_max]
        
    slopes = 0.5 * (country.diff(1) - country.diff(-1))
    ratios = slopes / country
    x = country.values[1:-1]
    y = ratios.values[1:-1]
    fig = plt.figure(figsize=(8, 8))
    ax = fig.add_subplot(1, 1, 1)
    _ = plt.plot(x, y, 'o')
    _ = ax.set_xlabel('D(t)')
    _ = ax.set_ylabel('Ratios of slopes to function values')
    
    return x, y
 ````
 
 2. linear regression
 
 ````
 def linear_regression(x, y):
    """ Find the coefficients of the linear function y = ax + b,  
        using a linear regression.
    """
    X = x.reshape(-1, 1) 
    reg = LinearRegression(fit_intercept=True, normalize=True)
    _ = reg.fit(X, y)
    a = reg.coef_[0]
    b = reg.intercept_
    y_hat = a * x + b
    fig = plt.figure(figsize=(8, 8))
    ax = fig.add_subplot(1, 1, 1)
    _ = plt.plot(x, y, 'o')
    _ = plt.plot(x, y_hat, '-', label='Linear regression')
    _ = ax.set_xlabel('D(t)')
    _ = ax.set_ylabel('Ratios of slopes to function values')
    _ = ax.legend()
    
    return a, b
 
 ````
 
 3. t0
 
 ````
 def plot_t0(a, b, country, death_min=0, death_max=None, t0=0):
    """ Find a value of t0 such that the logistic curve is as close 
        as possible to the data on the given interval.
    """
    k = b
    L = -b / a
    country = country[country > death_min]
    
    if death_max is not None:
        country = country[country < death_max]
        
    logis = L / (1. + np.exp(-k * (np.arange(len(country)) - t0)))
    fig = plt.figure(figsize=(8, 8))
    ax = fig.add_subplot(1, 1, 1)
    _ = plt.plot(logis, 'o')
    _ = plt.plot(country.values, 'd')
    
    return L, k
 
 ````
 
 4. logistic regression
 
 ````
 def logistic_regression(country, death_min, L, k, t0, days_before=30, days_after=30,
                  figsize=FS):
    """ Plot the logistic curve on an extended interval, 
        against the real data.
    """
    country_original = country.copy(deep=True)
    country = country[country > death_min]
    country = country.to_frame('Deaths')
    country_start = country.index.min()
    country_end = country.index.max()
    start = country_start - timedelta(days=days_before)
    end = country_end + timedelta(days=days_after)
    ix = pd.date_range(start=start, end=end, freq='D')
    country = country.reindex(ix)
    country['idx'] = np.arange(len(country))
    country['idx'] -= country.loc[country_start, 'idx']
    country['prediction'] = L / (1. + np.exp(-k * (country['idx'].values - t0)))
    ax = country['prediction'].plot(figsize=figsize, logy=False)
    _ = country_original[start:].plot(ax=ax, style='v')
    _ = ax.legend()
    plt.xlabel("Month")
    plt.ylabel("Deaths")
 
 ````
 
 ![Zozor](https://zupimages.net/up/21/04/xujk.png)
 
____ 
## Libraries used

* itertools
* timedelta
* numpy
* matplotlib
* pandas
* LinearRegression

____
