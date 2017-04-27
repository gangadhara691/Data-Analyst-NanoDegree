
# Statistics: The Science of Decisions Project by Gangadhara Naga Sai

Background Information

In a Stroop task, participants are presented with a list of words, with each word displayed in a color of ink. The participant’s task is to say out loud the color of the ink in which the word is printed. The task has two conditions: a congruent words condition, and an incongruent words condition. In the congruent words condition, the words being displayed are color words whose names match the colors in which they are printed: for example RED, BLUE. In the incongruent words condition, the words displayed are color words whose names do not match the colors in which they are printed: for example PURPLE, ORANGE. In each case, we measure the time it takes to name the ink colors in equally-sized lists. Each participant will go through and record a time from each condition.




```python
#Loading data
%matplotlib inline 
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import math

data = pd.read_csv("stroopdata.csv")
data
#The difference is calculated in the csv file itself
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Congruent</th>
      <th>Incongruent</th>
      <th>Difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12.079</td>
      <td>19.278</td>
      <td>-7.199</td>
    </tr>
    <tr>
      <th>1</th>
      <td>16.791</td>
      <td>18.741</td>
      <td>-1.950</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9.564</td>
      <td>21.214</td>
      <td>-11.650</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.630</td>
      <td>15.687</td>
      <td>-7.057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>14.669</td>
      <td>22.803</td>
      <td>-8.134</td>
    </tr>
    <tr>
      <th>5</th>
      <td>12.238</td>
      <td>20.878</td>
      <td>-8.640</td>
    </tr>
    <tr>
      <th>6</th>
      <td>14.692</td>
      <td>24.572</td>
      <td>-9.880</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.987</td>
      <td>17.394</td>
      <td>-8.407</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9.401</td>
      <td>20.762</td>
      <td>-11.361</td>
    </tr>
    <tr>
      <th>9</th>
      <td>14.480</td>
      <td>26.282</td>
      <td>-11.802</td>
    </tr>
    <tr>
      <th>10</th>
      <td>22.328</td>
      <td>24.524</td>
      <td>-2.196</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15.298</td>
      <td>18.644</td>
      <td>-3.346</td>
    </tr>
    <tr>
      <th>12</th>
      <td>15.073</td>
      <td>17.510</td>
      <td>-2.437</td>
    </tr>
    <tr>
      <th>13</th>
      <td>16.929</td>
      <td>20.330</td>
      <td>-3.401</td>
    </tr>
    <tr>
      <th>14</th>
      <td>18.200</td>
      <td>35.255</td>
      <td>-17.055</td>
    </tr>
    <tr>
      <th>15</th>
      <td>12.130</td>
      <td>22.158</td>
      <td>-10.028</td>
    </tr>
    <tr>
      <th>16</th>
      <td>18.495</td>
      <td>25.139</td>
      <td>-6.644</td>
    </tr>
    <tr>
      <th>17</th>
      <td>10.639</td>
      <td>20.429</td>
      <td>-9.790</td>
    </tr>
    <tr>
      <th>18</th>
      <td>11.344</td>
      <td>17.425</td>
      <td>-6.081</td>
    </tr>
    <tr>
      <th>19</th>
      <td>12.369</td>
      <td>34.288</td>
      <td>-21.919</td>
    </tr>
    <tr>
      <th>20</th>
      <td>12.944</td>
      <td>23.894</td>
      <td>-10.950</td>
    </tr>
    <tr>
      <th>21</th>
      <td>14.233</td>
      <td>17.960</td>
      <td>-3.727</td>
    </tr>
    <tr>
      <th>22</th>
      <td>19.710</td>
      <td>22.058</td>
      <td>-2.348</td>
    </tr>
    <tr>
      <th>23</th>
      <td>16.004</td>
      <td>21.157</td>
      <td>-5.153</td>
    </tr>
  </tbody>
</table>
</div>



Questions For Investigation


## 1. What is our independent variable? What is our dependent variable?

>Independent variable: the words list type (congruent words or incongruent words) 

>Dependent variable: the time taken to recognize the colors of ink in equally-number of word lists 




## 2. What is an appropriate set of hypotheses for this task? What kind of statistical test do you expect to perform? Justify your choices.

From the fact that our brain processes text faster than colour,when we do the congruent word test we are having dual information from both text and color but for incongruent words test those both dont match and cause a confusion in recognising the color.

>The $H_{O}$(null hypothesis) is mean time taken to recognize the colors of ink for congruent words is equal to or greater than the mean time for incongruent words, so one-tailed t test is to be conducted. The $H_{A}$ (alternative hypothesis) is the congruent words mean is less than the incongruent words mean. 

$$ H_{O} = \mu_{C} \geq \mu_{I} $$

$$ H_{A} = \mu_{C} <  \mu_{I} $$

>#### $ \mu_{C}$ is the mean of the time taken to recognize the color under the congruent condition

>#### $\mu_{I}$is the mean ofthe time taken to recognize the color  under the incongruent condition

### Dependent-samples one-tailed t-test is to be performed:


> We perform this test to find weather the time taken to recognize the congruent words is statistically less than the time taken to recognize the incongruent words for the total population.
>This test we are trying to assess whether the sample means are different because the two populations and population means are different or just by chance.


>T test because we are not having data of total populations mean or variance. And the size is less than 30 ,where cannot be approximated to normal distribution, so we cannot use z test.
- The above data is a sample from a population
- From the data it is clear that the same group has undergone through two treatments of congruent and incongruent tests,which are dependent samples

>One-sided  t test, because to recognize the colour of incogruent words seems difficult, form the fact that processing speed of text is much faster than color, i wanted to examine whether the time was significantly longer for incongruent test compared to congruent test. 



## 3. Report some descriptive statistics regarding this dataset. Include at least one measure of central tendency and at least one measure of variability.




```python
df=pd.DataFrame({"Mean":data.mean(),"Median":data.median(),"Variance":data.var(),"Standard deviation":data.std()})

df

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mean</th>
      <th>Median</th>
      <th>Standard deviation</th>
      <th>Variance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Congruent</th>
      <td>14.051125</td>
      <td>14.3565</td>
      <td>3.559358</td>
      <td>12.669029</td>
    </tr>
    <tr>
      <th>Incongruent</th>
      <td>22.015917</td>
      <td>21.0175</td>
      <td>4.797057</td>
      <td>23.011757</td>
    </tr>
    <tr>
      <th>Difference</th>
      <td>-7.964792</td>
      <td>-7.6665</td>
      <td>4.864827</td>
      <td>23.666541</td>
    </tr>
  </tbody>
</table>
</div>



> #### From the above table we can see :
- Central tendency of differences in groups -7.9648,
- Variability of groups 

>>Congruent groups
>> - Variance is 12.67
>> - Standard deviation is 3.55

>> Incongruent groups 
>> - Variance is 23.012
>> - Standard deviation is 4.8

>> Difference
>> - Variance is 23.67
>> - Standard deviation is 4.86





## 4. Provide one or two visualizations that show the distribution of the sample data. Write one or two sentences noting what you observe about the plot or plots.




```python
# We are comparing both incongruent and congruent data 
#Distplot divides the data into several bins and the occurance is shown as density of that value in that bin
import seaborn as sns
for a  in ["Congruent","Incongruent"]:
    sns.distplot(data[a], label=a)
plt.ylabel("Density")
plt.title('Histogram Comparision')  
plt.xlabel("Time taken to recognize")
plt.legend();
```


![png](output_8_0.png)


### From the above plot :
>- The congruent group appears normally distributed,
- The incongruent group appears to be bimodal, with 2 normal distributions.(this might be clear if we observe the total population)
- comparing both,incongruent distribution is having higher values as expected


```python
sns.factorplot( data=data[["Congruent","Incongruent"]], kind="box", size=7, aspect=.8)\
.set_xticklabels(["Congruent","Incongruent"])
plt.title('Boxplot Comparision')  
plt.ylabel("Time taken to recognize")
```




    <matplotlib.text.Text at 0xbf306a0>




![png](output_10_1.png)


### From the above boxplot:
- We can see two outliers for the incongruent test.
- The mean time taken for the incongruent test is higher than the congruent test


So lets conform by contucting the t test

## 5. Now, perform the statistical test and report your results. What is your confidence level and your critical statistic value? Do you reject the null hypothesis or fail to reject it? Come to a conclusion in terms of the experiment task. Did the results match up with your expectations?



>$ \mu_{Congruent} = 14.05113 $

>$ \mu_{Incongruent} = 22.01592$

>$ \mu_{Difference} = - 7.96479 $

>$Standard-Error_{Differences} = SE_{d} =\frac{\sigma}{\sqrt{n}}=\frac{4.864827}{\sqrt{24}}=0.993029$

>$ df = 𝑛 − 1 = 24 − 1 = 23$

>- t-critical value for a one-tailed test with $\alpha = 0.05$ and 𝑑𝑓 = 23 ,t-critical = −1.714(left tail)

>$t=\frac{\mu_{d}}{SEd}=\frac{ -7.96479}{0.993029}=-8.021$

>- The p-value for a t-statistic of -8.021 with df=23 is very small; it is $p < 0.00001$

>### Since -8.0211 < -1.714 , we Reject Null Hypothesis with 95% confidence.
>#### -  Concluding that form the fact that speed of processing of text is much faster than color, proving stroop effect to be true.



## Refrences:
- http://seaborn.pydata.org/tutorial/distributions.html
- https://en.wikipedia.org/wiki/Stroop_effect
- https://gist.github.com/wrobstory/c990c94fc4598a440e7f
