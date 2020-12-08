[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

**Exercise 1**   Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means. As a starting place, you can use chap03ex.ipynb.

```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
    
df_ch3 = nsfg.ReadFemResp()

numkids_pmf = thinkstats2.Pmf(df_ch3.numkdhh, label = "actual")
print("mean of the actual distribution {0:0.3f}".format(numkids_pmf.Mean()))

biased_numkids_pmf = BiasPmf(numkids_pmf, label = "observed_kids")
print("mean of the biased distribution {0:0.3f}".format(biased_numkids_pmf.Mean()))

thinkplot.PrePlot(2)
thinkplot.Pmfs([numkids_pmf, biased_numkids_pmf])
thinkplot.Show(xlabel = "number of kids", ylabel = "PMF", legend = True)
```

