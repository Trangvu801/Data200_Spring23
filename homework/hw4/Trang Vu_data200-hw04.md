# Data 200: Database Systems and Data Management for Data Analytics


# Homework 4: Pandas Operations

**Dickinson College**<br/>
**Spring 2023**<br/>
<font color='red'>**Due Date and Time:** Beginning of class on Tuesday, 3/7/2023 </font>
---
Please enter your name in the markdown cell below.

# Name: Trang Vu

# Tasks

- Review Ch8, pages 205-248 in the textbook.
- Complete the **Aggregating DataFrames** chapter of the **Data Manipulation with Pandas** course and **Data Merging Basics** chapter of the **Joining Data with Pandas** course on DataCamp.
- Commit and push your completed hw before the due date above.

# Exercises

Let's do an exploration of record times set in Mario Kart. This data is made available as part of Tidy Tuesday. A codebook is available at https://github.com/rfordatascience/tidytuesday/tree/master/data/2021/2021-05-25.

**Run the code cell below**, which loads in the data.


```python
import matplotlib.pyplot as plt
import pandas as pd

records = pd.read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-05-25/records.csv')
records
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
      <th>track</th>
      <th>type</th>
      <th>shortcut</th>
      <th>player</th>
      <th>system_played</th>
      <th>date</th>
      <th>time_period</th>
      <th>time</th>
      <th>record_duration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Luigi Raceway</td>
      <td>Three Lap</td>
      <td>No</td>
      <td>Salam</td>
      <td>NTSC</td>
      <td>1997-02-15</td>
      <td>2M 12.99S</td>
      <td>132.99</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Luigi Raceway</td>
      <td>Three Lap</td>
      <td>No</td>
      <td>Booth</td>
      <td>NTSC</td>
      <td>1997-02-16</td>
      <td>2M 9.99S</td>
      <td>129.99</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Luigi Raceway</td>
      <td>Three Lap</td>
      <td>No</td>
      <td>Salam</td>
      <td>NTSC</td>
      <td>1997-02-16</td>
      <td>2M 8.99S</td>
      <td>128.99</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Luigi Raceway</td>
      <td>Three Lap</td>
      <td>No</td>
      <td>Salam</td>
      <td>NTSC</td>
      <td>1997-02-28</td>
      <td>2M 6.99S</td>
      <td>126.99</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Luigi Raceway</td>
      <td>Three Lap</td>
      <td>No</td>
      <td>Gregg G</td>
      <td>NTSC</td>
      <td>1997-03-07</td>
      <td>2M 4.51S</td>
      <td>124.51</td>
      <td>54</td>
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
    </tr>
    <tr>
      <th>2329</th>
      <td>Rainbow Road</td>
      <td>Single Lap</td>
      <td>Yes</td>
      <td>MR</td>
      <td>PAL</td>
      <td>2018-04-13</td>
      <td>1M 56.56S</td>
      <td>116.56</td>
      <td>358</td>
    </tr>
    <tr>
      <th>2330</th>
      <td>Rainbow Road</td>
      <td>Single Lap</td>
      <td>Yes</td>
      <td>abney317</td>
      <td>PAL</td>
      <td>2019-04-06</td>
      <td>1M 56.53S</td>
      <td>116.53</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2331</th>
      <td>Rainbow Road</td>
      <td>Single Lap</td>
      <td>Yes</td>
      <td>MR</td>
      <td>PAL</td>
      <td>2019-04-10</td>
      <td>1M 56.52S</td>
      <td>116.52</td>
      <td>428</td>
    </tr>
    <tr>
      <th>2332</th>
      <td>Rainbow Road</td>
      <td>Single Lap</td>
      <td>Yes</td>
      <td>Dan</td>
      <td>PAL</td>
      <td>2020-06-11</td>
      <td>1M 56.48S</td>
      <td>116.48</td>
      <td>85</td>
    </tr>
    <tr>
      <th>2333</th>
      <td>Rainbow Road</td>
      <td>Single Lap</td>
      <td>Yes</td>
      <td>MR</td>
      <td>PAL</td>
      <td>2020-09-04</td>
      <td>1M 56.35S</td>
      <td>116.35</td>
      <td>175</td>
    </tr>
  </tbody>
</table>
<p>2334 rows × 9 columns</p>
</div>



This dataset consists of 2334 observations on the following variables. 


- `track`: </t>Track name <br>
- `type`: </t>Single or three lap record  <br>
- `shortcut`: </t>Shortcut or non-shortcut record  <br>
- `player`: </t>Player’s name  <br>
- `system_played`: </t>Used system (NTSC or PAL)<br>
- `date`: </t>World record date  <br>
- `time_period`: </t>Time as hms period  <br>
- `time`: </t>Time in seconds  <br>
- `record_duration`: </t>Record duration in days  <br>



<div class="exercise"><b>Exercise 1</b></div> 

Print and display information about the dataframe you have just loaded in, using info(). Here is my output below:
<code>
\<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2334 entries, 0 to 2333
Data columns (total 9 columns):
 \#   Column           Non-Null Count  Dtype  
\---  ------           --------------  -----  
 0   track            2334 non-null   object 
 1   type             2334 non-null   object 
 2   shortcut         2334 non-null   object 
 3   player           2334 non-null   object 
 4   system_played    2334 non-null   object 
 5   date             2334 non-null   object 
 6   time_period      2334 non-null   object 
 7   time             2334 non-null   float64
 8   record_duration  2334 non-null   int64  
dtypes: float64(1), int64(1), object(7)
memory usage: 164.2+ KB    
    </code>


```python
records.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2334 entries, 0 to 2333
    Data columns (total 9 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   track            2334 non-null   object 
     1   type             2334 non-null   object 
     2   shortcut         2334 non-null   object 
     3   player           2334 non-null   object 
     4   system_played    2334 non-null   object 
     5   date             2334 non-null   object 
     6   time_period      2334 non-null   object 
     7   time             2334 non-null   float64
     8   record_duration  2334 non-null   int64  
    dtypes: float64(1), int64(1), object(7)
    memory usage: 164.2+ KB


<div class="exercise"><b>Exercise 2</b></div> 

Compute and print the following information about the dataframe `records`: the descriptive statistics for the record duration in days (`record_duration`), the record time (`time`) by each track (`track`). You should use the `groupby()` function.
    
The output from my solution is as follows: <br>
<code>
time	record_duration
count	mean	std	min	25%	50%	75%	max	count	mean	std	min	25%	50%	75%	max
track																
Banshee Boardwalk	83.0	97.440602	40.201457	40.78	41.7850	124.420	125.7900	135.94	83.0	220.746988	368.822082	0.0	9.50	66.0	197.50	1694.0
Bowser's Castle	69.0	96.228116	44.796789	43.15	44.3800	132.280	133.8600	141.22	69.0	261.086957	444.011385	0.0	28.00	95.0	236.00	2499.0
Choco Mountain	148.0	70.786216	36.050534	17.29	38.6900	50.965	116.1425	127.96	148.0	240.736486	529.238297	0.0	7.00	32.0	188.00	2742.0
D.K.'s Jungle Parkway	180.0	70.985500	46.360088	21.35	42.4700	43.090	132.8125	156.44	180.0	199.122222	310.806298	0.0	7.00	78.0	246.00	2197.0
Frappe Snowland	180.0	58.590222	39.289745	23.61	38.2850	38.850	120.0450	131.43	180.0	219.727778	434.289400	0.0	5.75	59.5	196.00	2353.0
Kalimari Desert	169.0	76.911302	42.899116	38.96	39.3700	40.300	125.0900	134.22	169.0	207.526627	377.326546	0.0	6.00	36.0	186.00	1667.0
Koopa Troopa Beach	89.0	72.414831	31.764036	30.78	31.5800	95.470	96.5600	102.01	89.0	211.146067	464.299975	0.0	4.00	51.0	193.00	3042.0
Luigi Raceway	147.0	74.320816	38.467468	25.30	37.9500	44.970	118.0650	132.99	147.0	249.972789	530.215166	0.0	4.00	43.0	136.00	2842.0
Mario Raceway	160.0	54.195875	27.299417	27.62	27.7875	60.730	87.8200	95.06	160.0	246.800000	397.494619	0.0	20.00	91.5	309.25	2501.0
Moo Moo Farm	81.0	61.069012	30.046579	27.80	28.5800	86.000	88.1100	95.48	81.0	232.197531	351.818896	0.0	25.00	91.0	267.00	2103.0
Rainbow Road	179.0	205.273352	103.942052	50.38	117.3100	124.540	280.9400	375.83	179.0	198.905028	365.526044	0.0	3.00	35.0	229.50	2214.0
Royal Raceway	149.0	109.207785	53.834031	55.50	56.3900	119.630	171.9700	187.19	149.0	254.174497	494.810498	0.0	6.00	53.0	250.00	3022.0
Sherbet Land	143.0	78.143706	38.857519	37.72	38.5650	97.360	116.4650	124.00	143.0	191.538462	393.778156	0.0	6.50	31.0	150.50	2406.0
Toad's Turnpike	196.0	98.878878	54.126774	30.31	58.8450	60.850	177.9525	190.12	196.0	184.464286	381.856496	0.0	2.00	40.5	151.75	1897.0
Wario Stadium	201.0	132.035373	84.921671	14.59	86.4300	87.240	260.6700	280.34	201.0	184.124378	329.252015	0.0	2.00	19.0	200.00	2008.0
Yoshi Valley	160.0	55.580563	33.810687	31.25	31.7100	33.390	102.3350	120.65	160.0	280.856250	612.303619	0.0	8.00	60.5	181.25	3659.0</code>


```python
records.groupby('track').describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">time</th>
      <th colspan="8" halign="left">record_duration</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>track</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Banshee Boardwalk</th>
      <td>83.0</td>
      <td>97.440602</td>
      <td>40.201457</td>
      <td>40.78</td>
      <td>41.7850</td>
      <td>124.420</td>
      <td>125.7900</td>
      <td>135.94</td>
      <td>83.0</td>
      <td>220.746988</td>
      <td>368.822082</td>
      <td>0.0</td>
      <td>9.50</td>
      <td>66.0</td>
      <td>197.50</td>
      <td>1694.0</td>
    </tr>
    <tr>
      <th>Bowser's Castle</th>
      <td>69.0</td>
      <td>96.228116</td>
      <td>44.796789</td>
      <td>43.15</td>
      <td>44.3800</td>
      <td>132.280</td>
      <td>133.8600</td>
      <td>141.22</td>
      <td>69.0</td>
      <td>261.086957</td>
      <td>444.011385</td>
      <td>0.0</td>
      <td>28.00</td>
      <td>95.0</td>
      <td>236.00</td>
      <td>2499.0</td>
    </tr>
    <tr>
      <th>Choco Mountain</th>
      <td>148.0</td>
      <td>70.786216</td>
      <td>36.050534</td>
      <td>17.29</td>
      <td>38.6900</td>
      <td>50.965</td>
      <td>116.1425</td>
      <td>127.96</td>
      <td>148.0</td>
      <td>240.736486</td>
      <td>529.238297</td>
      <td>0.0</td>
      <td>7.00</td>
      <td>32.0</td>
      <td>188.00</td>
      <td>2742.0</td>
    </tr>
    <tr>
      <th>D.K.'s Jungle Parkway</th>
      <td>180.0</td>
      <td>70.985500</td>
      <td>46.360088</td>
      <td>21.35</td>
      <td>42.4700</td>
      <td>43.090</td>
      <td>132.8125</td>
      <td>156.44</td>
      <td>180.0</td>
      <td>199.122222</td>
      <td>310.806298</td>
      <td>0.0</td>
      <td>7.00</td>
      <td>78.0</td>
      <td>246.00</td>
      <td>2197.0</td>
    </tr>
    <tr>
      <th>Frappe Snowland</th>
      <td>180.0</td>
      <td>58.590222</td>
      <td>39.289745</td>
      <td>23.61</td>
      <td>38.2850</td>
      <td>38.850</td>
      <td>120.0450</td>
      <td>131.43</td>
      <td>180.0</td>
      <td>219.727778</td>
      <td>434.289400</td>
      <td>0.0</td>
      <td>5.75</td>
      <td>59.5</td>
      <td>196.00</td>
      <td>2353.0</td>
    </tr>
    <tr>
      <th>Kalimari Desert</th>
      <td>169.0</td>
      <td>76.911302</td>
      <td>42.899116</td>
      <td>38.96</td>
      <td>39.3700</td>
      <td>40.300</td>
      <td>125.0900</td>
      <td>134.22</td>
      <td>169.0</td>
      <td>207.526627</td>
      <td>377.326546</td>
      <td>0.0</td>
      <td>6.00</td>
      <td>36.0</td>
      <td>186.00</td>
      <td>1667.0</td>
    </tr>
    <tr>
      <th>Koopa Troopa Beach</th>
      <td>89.0</td>
      <td>72.414831</td>
      <td>31.764036</td>
      <td>30.78</td>
      <td>31.5800</td>
      <td>95.470</td>
      <td>96.5600</td>
      <td>102.01</td>
      <td>89.0</td>
      <td>211.146067</td>
      <td>464.299975</td>
      <td>0.0</td>
      <td>4.00</td>
      <td>51.0</td>
      <td>193.00</td>
      <td>3042.0</td>
    </tr>
    <tr>
      <th>Luigi Raceway</th>
      <td>147.0</td>
      <td>74.320816</td>
      <td>38.467468</td>
      <td>25.30</td>
      <td>37.9500</td>
      <td>44.970</td>
      <td>118.0650</td>
      <td>132.99</td>
      <td>147.0</td>
      <td>249.972789</td>
      <td>530.215166</td>
      <td>0.0</td>
      <td>4.00</td>
      <td>43.0</td>
      <td>136.00</td>
      <td>2842.0</td>
    </tr>
    <tr>
      <th>Mario Raceway</th>
      <td>160.0</td>
      <td>54.195875</td>
      <td>27.299417</td>
      <td>27.62</td>
      <td>27.7875</td>
      <td>60.730</td>
      <td>87.8200</td>
      <td>95.06</td>
      <td>160.0</td>
      <td>246.800000</td>
      <td>397.494619</td>
      <td>0.0</td>
      <td>20.00</td>
      <td>91.5</td>
      <td>309.25</td>
      <td>2501.0</td>
    </tr>
    <tr>
      <th>Moo Moo Farm</th>
      <td>81.0</td>
      <td>61.069012</td>
      <td>30.046579</td>
      <td>27.80</td>
      <td>28.5800</td>
      <td>86.000</td>
      <td>88.1100</td>
      <td>95.48</td>
      <td>81.0</td>
      <td>232.197531</td>
      <td>351.818896</td>
      <td>0.0</td>
      <td>25.00</td>
      <td>91.0</td>
      <td>267.00</td>
      <td>2103.0</td>
    </tr>
    <tr>
      <th>Rainbow Road</th>
      <td>179.0</td>
      <td>205.273352</td>
      <td>103.942052</td>
      <td>50.38</td>
      <td>117.3100</td>
      <td>124.540</td>
      <td>280.9400</td>
      <td>375.83</td>
      <td>179.0</td>
      <td>198.905028</td>
      <td>365.526044</td>
      <td>0.0</td>
      <td>3.00</td>
      <td>35.0</td>
      <td>229.50</td>
      <td>2214.0</td>
    </tr>
    <tr>
      <th>Royal Raceway</th>
      <td>149.0</td>
      <td>109.207785</td>
      <td>53.834031</td>
      <td>55.50</td>
      <td>56.3900</td>
      <td>119.630</td>
      <td>171.9700</td>
      <td>187.19</td>
      <td>149.0</td>
      <td>254.174497</td>
      <td>494.810498</td>
      <td>0.0</td>
      <td>6.00</td>
      <td>53.0</td>
      <td>250.00</td>
      <td>3022.0</td>
    </tr>
    <tr>
      <th>Sherbet Land</th>
      <td>143.0</td>
      <td>78.143706</td>
      <td>38.857519</td>
      <td>37.72</td>
      <td>38.5650</td>
      <td>97.360</td>
      <td>116.4650</td>
      <td>124.00</td>
      <td>143.0</td>
      <td>191.538462</td>
      <td>393.778156</td>
      <td>0.0</td>
      <td>6.50</td>
      <td>31.0</td>
      <td>150.50</td>
      <td>2406.0</td>
    </tr>
    <tr>
      <th>Toad's Turnpike</th>
      <td>196.0</td>
      <td>98.878878</td>
      <td>54.126774</td>
      <td>30.31</td>
      <td>58.8450</td>
      <td>60.850</td>
      <td>177.9525</td>
      <td>190.12</td>
      <td>196.0</td>
      <td>184.464286</td>
      <td>381.856496</td>
      <td>0.0</td>
      <td>2.00</td>
      <td>40.5</td>
      <td>151.75</td>
      <td>1897.0</td>
    </tr>
    <tr>
      <th>Wario Stadium</th>
      <td>201.0</td>
      <td>132.035373</td>
      <td>84.921671</td>
      <td>14.59</td>
      <td>86.4300</td>
      <td>87.240</td>
      <td>260.6700</td>
      <td>280.34</td>
      <td>201.0</td>
      <td>184.124378</td>
      <td>329.252015</td>
      <td>0.0</td>
      <td>2.00</td>
      <td>19.0</td>
      <td>200.00</td>
      <td>2008.0</td>
    </tr>
    <tr>
      <th>Yoshi Valley</th>
      <td>160.0</td>
      <td>55.580563</td>
      <td>33.810687</td>
      <td>31.25</td>
      <td>31.7100</td>
      <td>33.390</td>
      <td>102.3350</td>
      <td>120.65</td>
      <td>160.0</td>
      <td>280.856250</td>
      <td>612.303619</td>
      <td>0.0</td>
      <td>8.00</td>
      <td>60.5</td>
      <td>181.25</td>
      <td>3659.0</td>
    </tr>
  </tbody>
</table>
</div>



<div class="exercise"><b>Exercise 3</b></div> 

Compute and print the record time (`time`) set in each track (`track`). You should use the `groupby()` function. Here is my output below:

<code>
track
Banshee Boardwalk        40.78
Bowser's Castle          43.15
Choco Mountain           17.29
D.K.'s Jungle Parkway    21.35
Frappe Snowland          23.61
Kalimari Desert          38.96
Koopa Troopa Beach       30.78
Luigi Raceway            25.30
Mario Raceway            27.62
Moo Moo Farm             27.80
Rainbow Road             50.38
Royal Raceway            55.50
Sherbet Land             37.72
Toad's Turnpike          30.31
Wario Stadium            14.59
Yoshi Valley             31.25
Name: time, dtype: float64</code>


```python
records.groupby("track").min().time
```




    track
    Banshee Boardwalk        40.78
    Bowser's Castle          43.15
    Choco Mountain           17.29
    D.K.'s Jungle Parkway    21.35
    Frappe Snowland          23.61
    Kalimari Desert          38.96
    Koopa Troopa Beach       30.78
    Luigi Raceway            25.30
    Mario Raceway            27.62
    Moo Moo Farm             27.80
    Rainbow Road             50.38
    Royal Raceway            55.50
    Sherbet Land             37.72
    Toad's Turnpike          30.31
    Wario Stadium            14.59
    Yoshi Valley             31.25
    Name: time, dtype: float64



<div class="exercise"><b>Exercise 4</b></div> 

Compute and print the Top 10 players with the longest unbroken record and the day(s) it took for their record to be broken (in any track). You should use the `groupby()` function. Here is my output below:

<code>
player
Alex G       3659
VAJ          3103
MJ           3042
Troy         3022
Greg I       2682
Michael F    2623
Karlo        2537
Luke B       2501
Myles        2284
TJL          2103
Name: record_duration, dtype: int64</code>


```python
records.groupby("track").max().record_duration
```




    track
    Banshee Boardwalk        1694
    Bowser's Castle          2499
    Choco Mountain           2742
    D.K.'s Jungle Parkway    2197
    Frappe Snowland          2353
    Kalimari Desert          1667
    Koopa Troopa Beach       3042
    Luigi Raceway            2842
    Mario Raceway            2501
    Moo Moo Farm             2103
    Rainbow Road             2214
    Royal Raceway            3022
    Sherbet Land             2406
    Toad's Turnpike          1897
    Wario Stadium            2008
    Yoshi Valley             3659
    Name: record_duration, dtype: int64




```python
records.groupby("player").max().record_duration.sort_values(ascending=False)[0:10]
```




    player
    Alex G       3659
    VAJ          3103
    MJ           3042
    Troy         3022
    Greg I       2682
    Michael F    2623
    Karlo        2537
    Luke B       2501
    Myles        2284
    TJL          2103
    Name: record_duration, dtype: int64



<div class="exercise"><b>Exercise 5</b></div> 

Run the following line which creates a `year` column from the `date` column.


```python
records['year'] = records['date'].str[0:4]
```

Find the average `record time` and `record_duration` across years. Do you see an overall trend? Here is my output:

<code>            time  record_duration
year                             
1997   93.283349        91.330144
1998   93.714252        49.128609
1999   87.689314       135.249097
2000   77.343563       459.000000
2001   92.752727       344.545455
2002   92.183061       288.306122
2003   83.133162       247.117647
2004   99.601688       347.337662
2005   90.517222       413.911111
2006  105.006731       654.519231
2007   57.089583       348.416667
2008   82.310000      1237.400000
2009   92.757500       449.437500
2010   74.168400       441.800000
2011   95.897183       177.183099
2012   93.653333       318.086420
2013   77.365859       465.787879
2014  101.450333       230.966667
2015   95.659701       241.522388
2016  117.479020       191.068627
2017  107.327258       284.596774
2018   82.574805       290.207792
2019  111.825789       267.456140
2020   76.606471        59.490196
2021   62.377255        15.705882 </code>


```python
print(records.groupby("year").mean())
```

                time  record_duration
    year                             
    1997   93.283349        91.330144
    1998   93.714252        49.128609
    1999   87.689314       135.249097
    2000   77.343563       459.000000
    2001   92.752727       344.545455
    2002   92.183061       288.306122
    2003   83.133162       247.117647
    2004   99.601688       347.337662
    2005   90.517222       413.911111
    2006  105.006731       654.519231
    2007   57.089583       348.416667
    2008   82.310000      1237.400000
    2009   92.757500       449.437500
    2010   74.168400       441.800000
    2011   95.897183       177.183099
    2012   93.653333       318.086420
    2013   77.365859       465.787879
    2014  101.450333       230.966667
    2015   95.659701       241.522388
    2016  117.479020       191.068627
    2017  107.327258       284.596774
    2018   82.574805       290.207792
    2019  111.825789       267.456140
    2020   76.606471        59.490196
    2021   62.377255        15.705882


<div class="exercise"><b>Exercise 6: Concatenating Along the Row Dimension</b></div> 

In the hw directory, you will find two csv files, `educationTop.csv` and `educationBottom.csv`, both based on data hosted by www.census.gov. Both have the same columns, and each row is a U.S. metropolitan area, with data on population, education, and unemployment. The first csv file contains metropolitan areas starting with A-K, and the second starting with L-Z.

In the code cell below, write Python code to do the following.<br>

1. Import the Pandas library
1.  Read in the file `educationTop.csv`, using the column `Id` as the index, and assign it to the data frame `ed_top_df`. **Note** that you can use the `index_col='Id'` as a parameter to `pd.read_csv()` to set the index.<br>
1.  Read in the file `educationBottom.csv`, using the column `Id` as the index, and assign it to the data frame `ed_bottom_df`.<br>
1.  Concatenate these two data frames along the row dimension (with `ed_top_df` on top), and call the result `educationDF`.
1.  Print `ed_top_df.shape`, `ed_bottom_df.shape`, and `educationDF.shape`, mimicking my output below.
1.  Print the first five rows of `educationDF` for columns indexed 0 and 1 using the command `print(educationDF.head().iloc[:,:2])`.

The output from my solution is:<br>
<code>
The shape of ed_top_df is (176, 59)
The shape of ed_bottom_df is (190, 59)
The shape of educationDF is (366, 59)
</code><code>
                                    Geography  Estimate; Total:
Id                                                             
10180                  Abilene, TX Metro Area             82270
10420                    Akron, OH Metro Area            369311
10500                   Albany, GA Metro Area             78159
10580  Albany-Schenectady-Troy, NY Metro Area            466236
10740              Albuquerque, NM Metro Area            476942</code>


```python
import pandas as pd
ed_top_df = pd.read_csv('educationTop.csv', index_col='Id')
ed_bottom_df = pd.read_csv('educationBottom.csv', index_col='Id')

educationDF = pd.concat([ed_top_df, ed_bottom_df], axis=0)

print('The shape of ed_top_df is ' + str(ed_top_df.shape))
print('The shape of ed_bottom_df is ' + str(ed_bottom_df.shape))
print('The shape of educationDF is ' + str(educationDF.shape))
print()
print(educationDF.head().iloc[:,:2])
```

    The shape of ed_top_df is (176, 59)
    The shape of ed_bottom_df is (190, 59)
    The shape of educationDF is (366, 59)
    
                                        Geography  Estimate; Total:
    Id                                                             
    10180                  Abilene, TX Metro Area             82270
    10420                    Akron, OH Metro Area            369311
    10500                   Albany, GA Metro Area             78159
    10580  Albany-Schenectady-Troy, NY Metro Area            466236
    10740              Albuquerque, NM Metro Area            476942


<div class="exercise"><b>Exercise 7: Merging Data Frames with Merge</b></div> 

We are once again going to consider the data sets `educationLeftJ.csv` and `educationRightJ.csv`, however, we will read them in without a meaningful index.  That is, we will not assign an index when using the `read_csv()` function.

1.  Read in the file `educationLeftJ.csv` with no meaningful index and assign it to the data frame `eduLeft`.<br>
1.  Read in the file `educationRightJ.csv` with no meaningful index and assign it to the data frame `eduRight`.<br>
1.  Starting from `eduLeft`, do an *inner merge* along the column `Geography`, storing your answer as `dfJ3`.
1.  Print `dfJ3.shape`, mimicking my output below.

The output from my solution is:<br>
<code>
The shape of dfJ3 is (152, 25)
</code><code>


```python
eduLeft = pd.read_csv('educationLeftJ.csv')
eduRight = pd.read_csv('educationRightJ.csv')

dfJ3 = pd.merge(eduLeft, eduRight, on='Geography', how='inner' )
print('The shape of dfJ3 is ' + str(dfJ3.shape))
```

    The shape of dfJ3 is (152, 25)

