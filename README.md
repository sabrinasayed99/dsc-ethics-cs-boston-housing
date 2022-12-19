# Data Science Ethics - Sensitive Features Case Study

## Introduction
In the previous lesson, we discussed the Boston Housing data set and some of the problems inherent to it. In this lab, we are going to explore the nitty-gritty about why the Boston Housing data set is so problematic so you can spot __sensitive features__ and handle them accordingly. We will also touch on __data integrity issues__, a topic that we will explore in further detail in future lessons. 

## Learning Objectives
You will be able to:

* Download and read the Boston Housing data set from GitHub
* Identify and describe common data integrity issues
* Identify and describe sensitive features and possible negative impacts
* Discuss the reasons why the Boston Housing Data set is not an appropriate sample data set

## Load the Boston Housing Data Set
Due to the issues we will discuss in this lab, the Boston Housing Data set is no longer available in Seaborn as a sample data set. However, you can still access this data set on GitHub. Run the code cells below to import the Boston Housing data set from GitHub.


```python
import pandas as pd
df = pd.read_csv('https://raw.githubusercontent.com/selva86/datasets/master/BostonHousing.csv')
```


```python
df
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
      <th>crim</th>
      <th>zn</th>
      <th>indus</th>
      <th>chas</th>
      <th>nox</th>
      <th>rm</th>
      <th>age</th>
      <th>dis</th>
      <th>rad</th>
      <th>tax</th>
      <th>ptratio</th>
      <th>b</th>
      <th>lstat</th>
      <th>medv</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.00632</td>
      <td>18.0</td>
      <td>2.31</td>
      <td>0</td>
      <td>0.538</td>
      <td>6.575</td>
      <td>65.2</td>
      <td>4.0900</td>
      <td>1</td>
      <td>296</td>
      <td>15.3</td>
      <td>396.90</td>
      <td>4.98</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.02731</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>6.421</td>
      <td>78.9</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242</td>
      <td>17.8</td>
      <td>396.90</td>
      <td>9.14</td>
      <td>21.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.02729</td>
      <td>0.0</td>
      <td>7.07</td>
      <td>0</td>
      <td>0.469</td>
      <td>7.185</td>
      <td>61.1</td>
      <td>4.9671</td>
      <td>2</td>
      <td>242</td>
      <td>17.8</td>
      <td>392.83</td>
      <td>4.03</td>
      <td>34.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.03237</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>6.998</td>
      <td>45.8</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222</td>
      <td>18.7</td>
      <td>394.63</td>
      <td>2.94</td>
      <td>33.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.06905</td>
      <td>0.0</td>
      <td>2.18</td>
      <td>0</td>
      <td>0.458</td>
      <td>7.147</td>
      <td>54.2</td>
      <td>6.0622</td>
      <td>3</td>
      <td>222</td>
      <td>18.7</td>
      <td>396.90</td>
      <td>5.33</td>
      <td>36.2</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>501</th>
      <td>0.06263</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0</td>
      <td>0.573</td>
      <td>6.593</td>
      <td>69.1</td>
      <td>2.4786</td>
      <td>1</td>
      <td>273</td>
      <td>21.0</td>
      <td>391.99</td>
      <td>9.67</td>
      <td>22.4</td>
    </tr>
    <tr>
      <th>502</th>
      <td>0.04527</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0</td>
      <td>0.573</td>
      <td>6.120</td>
      <td>76.7</td>
      <td>2.2875</td>
      <td>1</td>
      <td>273</td>
      <td>21.0</td>
      <td>396.90</td>
      <td>9.08</td>
      <td>20.6</td>
    </tr>
    <tr>
      <th>503</th>
      <td>0.06076</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0</td>
      <td>0.573</td>
      <td>6.976</td>
      <td>91.0</td>
      <td>2.1675</td>
      <td>1</td>
      <td>273</td>
      <td>21.0</td>
      <td>396.90</td>
      <td>5.64</td>
      <td>23.9</td>
    </tr>
    <tr>
      <th>504</th>
      <td>0.10959</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0</td>
      <td>0.573</td>
      <td>6.794</td>
      <td>89.3</td>
      <td>2.3889</td>
      <td>1</td>
      <td>273</td>
      <td>21.0</td>
      <td>393.45</td>
      <td>6.48</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>505</th>
      <td>0.04741</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0</td>
      <td>0.573</td>
      <td>6.030</td>
      <td>80.8</td>
      <td>2.5050</td>
      <td>1</td>
      <td>273</td>
      <td>21.0</td>
      <td>396.90</td>
      <td>7.88</td>
      <td>11.9</td>
    </tr>
  </tbody>
</table>
<p>506 rows × 14 columns</p>
</div>



## Sensitive Features: "B"
The feature that has received the most scrutiny with respect to the Boston Housing Data set is the `B` feature. So why is the "B" feature such an issue?

One clue as to the reason why this feature is so problematic can be gleaned from the original description of this feature in the meta-data:
```
'1000(Bk — 0.63)² where Bk is the proportion of blacks(sic) by town'
```

### Sociological Issues
Beyond the cringe-worthy and dated language, from a sociological perspective there are several problems.

#### Implicit Bias 
The intentions of the designers of the study was to control for factors that might influence the price of a home to isolate for their target of clean air. **However, by including a measurement of the concentration of *exclusively black people* it implicitly suggests that the *presence of black people and not racism* is what negatively impacts home values.

#### Discriminatory Proxies
While using race as a proxy *can* have a benefit in the proper context. For example, if we wanted to improve equity in education, it might be helpful to understand the relationship between different racial populations and quality of the education offered in their area. However, without proper context, some features can be interpreted in discriminatory or harmful ways. 

### Statistical Issues
In addition to the harmful implications of the manner 

### Your Turn: Identifying Potential Discriminatory Proxies
1. Run the code cell below to view the columns in the Boston Housing data set. 


```python
df.columns
```




    Index(['crim', 'zn', 'indus', 'chas', 'nox', 'rm', 'age', 'dis', 'rad', 'tax',
           'ptratio', 'b', 'lstat', 'medv'],
          dtype='object')



2. Next, take a look at the image below which is extract from the 1976 paper that utilized the Boston Housing Data set. Can you identify any features that juxtaposed with race might create a fallacious argument for racist ideas? Type your response below the image.

<p>
<div>
    <center>
<table><tr><td>
<img src="https://curriculum-content.s3.amazonaws.com/data-science/images/images/ethics/lab1/boston-1.png" alt="Image of the sheets tab in the lower left corner of the Tableau Data Source Page, with the Left Pane and Canvas visible." alt="This is the alt-text for the image." style="width: 700px;"/>
</td></tr></table>
    </center>
</div>

### Potentially Discriminatory Proxies
* Proxy 1
* Proxy 2

## Summary
While the intentions of the study designers may not have been racially motivated, they were not sensitive to the potential detrimental consequences of the features they selected for their study. They failed use caution when including the "B" feature which led to the misappropriation of the data set over the course of its life as an educational tool. They did not consider how the set of features without the appropriate context could reinforce negative stereotypes about black communities. 
