[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

**Exercise 1**  The distribution of income is famously skewed to the right. In this exercise, we’ll measure how strong that skew is.
The Current Population Survey (CPS) is a joint effort of the Bureau of Labor Statistics and the Census Bureau to study income and related variables. 
Compute the median, mean, skewness and Pearson’s skewness of the resulting sample. What fraction of households reports a taxable income below the mean? How do the results depend on the assumed upper bound?

```python
import hinc
import hinc2
import numpy as np
df_ch6 = hinc.ReadData()

def InterpolateSample(df, log_upper=6.0):
    # compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    # get the lower bounds by shifting the upper bound and filling in
    # the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    # plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper
    
    # use the freq column to generate the right number of values in
    # each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, int(row.freq))
        arrays.append(vals)

    # collect the arrays into a single sample
    log_sample = np.concatenate(arrays)
    return log_sample
    
df_trans = InterpolateSample(df_ch6)
df_trans2 = np.power(10, df_trans)
median = np.median(df_trans2)
mean = df_trans2.mean()
skewness = thinkstats2.Skewness(df_trans2)
Pearson_skewness = thinkstats2.PearsonMedianSkewness(df_trans2)
cdf = thinkstats2.Cdf(df_trans2)
prob_mean = cdf.Prob(mean)
```

The **median** of the sample is 51226.93.

The **mean** of the sample is 74278.71.

The **skewness** of the sample is 4.95.

The **Pearson's skewness** of the sample is 0.736.

The **fraction of households reporting a taxable income below mean** is 0.66.

The median would not be affected by the assumed upper bound. However, skewness, Pearson's skewness, and mean would be affected. A upper bound of 100 millions instead of 1 million would increase the mean dramatically, and extend the distribution to the right. 
