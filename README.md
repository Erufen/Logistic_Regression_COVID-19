# Logistic Regression with dataset of COVID-19 

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
