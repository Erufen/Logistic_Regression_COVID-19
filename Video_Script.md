# Video Script

_________
![Zozor](https://zupimages.net/up/21/04/1zue.jpg)
__________



![Zozor](https://zupimages.net/up/21/04/v5fp.jpg)

````
Hello.
I will introduce you to a fundamental classification technique: logistic regression.
````


![Zozor](https://zupimages.net/up/21/04/j7hu.jpg)

````
In summary, there will be:

1st: a short introduction to this technique

2nd: a Python implementation that will give you a simplistic and naïve approach to 
the possible fit of the logistic curve to process COVID-19 data

3rd: a conclusion on all that was said during the presentation

And finally, the bibliography used for this presentation.
````

![Zozor](https://zupimages.net/up/21/04/sv1u.jpg)

````
By definition, a logistic curve is represented as an S (as in the example on the right) 
and its interval is defined between 0 and 1.

But in our example, the curve will not take this interval into account. It will be adapted to the experience.

This technique has several advantages, such as, for example:

    1. ease of use and interpretation.

    2. available on all conventional data processing software.

    3. results obtained have a good power of generalization.
````

![Zozor](https://zupimages.net/up/21/04/jqyq.jpg)

````
This is the mathematical formula for the logistic curve that was used for the construction of 
the graphs that I will present to you in the experiment which follows.
````

![Zozor](https://zupimages.net/up/21/04/nmmf.jpg)

````
The first thing to do is import the libraries needed to perform the experiment. 
So we need numpy, matplotlib and pandas for the most famous.

Next, we need to import an official dataset. You can see a snippet of the data 
it contains in the table to your right. What will interest us is in the last columns 
whose data represent the number of deaths per day.
````

![Zozor](https://zupimages.net/up/21/04/lwww.jpg)

````
Here is presented the number of deaths due to covid for 4 countries which are: Italy, Spain, France and UK.

The construction of this graph is rather easy to understand.

First, we retrieve the Province / State, Lat and Long columns to group them 
together with the corresponding Country / Region. 

Then, we associate the number of deaths for each country. 

Finally, you can choose the name of the countries that you want to display, 
as well as the moment when the curve should start.

Here it starts in September 2020.

To be able to obtain the final logistic curve, we must proceed to 3 preliminary steps which are:
````

![Zozor](https://zupimages.net/up/21/04/naej.jpg)

````
First step:
Calculation of ratios according to the number of deaths: this function is used to calculate 
the slope according to the number of deaths in an interval grouping together all the data
````

![Zozor](https://zupimages.net/up/21/04/uf9l.jpg)

````
and in a smaller interval with a minimum number of deaths equal to two hundred.
````

![Zozor](https://zupimages.net/up/21/04/w9re.jpg)

````
Second step is the construction of the regression line whose equation is y = a x + b
````

![Zozor](https://zupimages.net/up/21/04/ryky.jpg)

````
Third step is the determination of t0:
This function is used to return the values of the variables L and k.
It makes it possible to construct the sigmoid as close as possible to the curve of the real data.

The t0’s value is empirical.
````

![Zozor](https://zupimages.net/up/21/04/6rrk.jpg)

````
Finally, we obtain the logistic curve which must predict the number of deaths as a function of months.
In the logistic_regression function, we find the equation at the start of the country prediction variable.

We can see in the graph to the right that we exceeded the predictions in mid-November.
````

![Zozor](https://zupimages.net/up/21/04/gkmg.jpg)

````
Here are the 3 other countries with actual data (since March 2020) and the logistic prediction curve.

We can thus say that the number of deaths was predictable in UK.

I'll let you guess what might happen next …
````

![Zozor](https://zupimages.net/up/21/04/vmfv.jpg)

````
To conclude, logistic regression serves:

to build a simple mathematical model

and

can be empirically adapted to special datasets

That’s why it’s so popular in ML.
````

![Zozor](https://zupimages.net/up/21/04/9ah6.jpg)

````
[No text]
````

![Zozor](https://zupimages.net/up/21/04/fxwl.jpg)

````
[No text]
````
