

```python
import pandas as pd
```

## imports for Python, Pandas


```python
import json
from pandas.io.json import json_normalize
```

****
## JSON exercise

Using data in file 'data/world_bank_projects.json' and the techniques demonstrated above,
1. Find the 10 countries with most projects
2. Find the top 10 major project themes (using column 'mjtheme_namecode')
3. In 2. above you will notice that some entries have only the code and the name is missing. Create a dataframe with the missing names filled in.


```python
# Explore input JSON
pd_projects = pd.read_json('data/world_bank_projects.json')
pd_projects.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>_id</th>
      <th>approvalfy</th>
      <th>board_approval_month</th>
      <th>boardapprovaldate</th>
      <th>borrower</th>
      <th>closingdate</th>
      <th>country_namecode</th>
      <th>countrycode</th>
      <th>countryname</th>
      <th>countryshortname</th>
      <th>...</th>
      <th>sectorcode</th>
      <th>source</th>
      <th>status</th>
      <th>supplementprojectflg</th>
      <th>theme1</th>
      <th>theme_namecode</th>
      <th>themecode</th>
      <th>totalamt</th>
      <th>totalcommamt</th>
      <th>url</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>{'$oid': '52b213b38594d8a2be17c780'}</td>
      <td>1999</td>
      <td>November</td>
      <td>2013-11-12T00:00:00Z</td>
      <td>FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA</td>
      <td>2018-07-07T00:00:00Z</td>
      <td>Federal Democratic Republic of Ethiopia!$!ET</td>
      <td>ET</td>
      <td>Federal Democratic Republic of Ethiopia</td>
      <td>Ethiopia</td>
      <td>...</td>
      <td>ET,BS,ES,EP</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 100, 'Name': 'Education for all'}</td>
      <td>[{'code': '65', 'name': 'Education for all'}]</td>
      <td>65</td>
      <td>130000000</td>
      <td>130000000</td>
      <td>http://www.worldbank.org/projects/P129828/ethi...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>{'$oid': '52b213b38594d8a2be17c781'}</td>
      <td>2015</td>
      <td>November</td>
      <td>2013-11-04T00:00:00Z</td>
      <td>GOVERNMENT OF TUNISIA</td>
      <td>NaN</td>
      <td>Republic of Tunisia!$!TN</td>
      <td>TN</td>
      <td>Republic of Tunisia</td>
      <td>Tunisia</td>
      <td>...</td>
      <td>BZ,BS</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 30, 'Name': 'Other economic manage...</td>
      <td>[{'code': '24', 'name': 'Other economic manage...</td>
      <td>54,24</td>
      <td>0</td>
      <td>4700000</td>
      <td>http://www.worldbank.org/projects/P144674?lang=en</td>
    </tr>
    <tr>
      <th>2</th>
      <td>{'$oid': '52b213b38594d8a2be17c782'}</td>
      <td>2014</td>
      <td>November</td>
      <td>2013-11-01T00:00:00Z</td>
      <td>MINISTRY OF FINANCE AND ECONOMIC DEVEL</td>
      <td>NaN</td>
      <td>Tuvalu!$!TV</td>
      <td>TV</td>
      <td>Tuvalu</td>
      <td>Tuvalu</td>
      <td>...</td>
      <td>TI</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>Y</td>
      <td>{'Percent': 46, 'Name': 'Regional integration'}</td>
      <td>[{'code': '47', 'name': 'Regional integration'...</td>
      <td>52,81,25,47</td>
      <td>6060000</td>
      <td>6060000</td>
      <td>http://www.worldbank.org/projects/P145310?lang=en</td>
    </tr>
    <tr>
      <th>3</th>
      <td>{'$oid': '52b213b38594d8a2be17c783'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-31T00:00:00Z</td>
      <td>MIN. OF PLANNING AND INT'L COOPERATION</td>
      <td>NaN</td>
      <td>Republic of Yemen!$!RY</td>
      <td>RY</td>
      <td>Republic of Yemen</td>
      <td>Yemen, Republic of</td>
      <td>...</td>
      <td>JB</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 50, 'Name': 'Participation and civ...</td>
      <td>[{'code': '57', 'name': 'Participation and civ...</td>
      <td>59,57</td>
      <td>0</td>
      <td>1500000</td>
      <td>http://www.worldbank.org/projects/P144665?lang=en</td>
    </tr>
    <tr>
      <th>4</th>
      <td>{'$oid': '52b213b38594d8a2be17c784'}</td>
      <td>2014</td>
      <td>October</td>
      <td>2013-10-31T00:00:00Z</td>
      <td>MINISTRY OF FINANCE</td>
      <td>2019-04-30T00:00:00Z</td>
      <td>Kingdom of Lesotho!$!LS</td>
      <td>LS</td>
      <td>Kingdom of Lesotho</td>
      <td>Lesotho</td>
      <td>...</td>
      <td>FH,YW,YZ</td>
      <td>IBRD</td>
      <td>Active</td>
      <td>N</td>
      <td>{'Percent': 30, 'Name': 'Export development an...</td>
      <td>[{'code': '45', 'name': 'Export development an...</td>
      <td>41,45</td>
      <td>13100000</td>
      <td>13100000</td>
      <td>http://www.worldbank.org/projects/P144933/seco...</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 50 columns</p>
</div>




```python
json_projects = json.load((open('data/world_bank_projects.json')))
# Normalize mjtheme_namecode JSON field
json_df = json_normalize(json_projects, 'mjtheme_namecode', ['countryshortname'])
json_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>code</th>
      <th>name</th>
      <th>countryshortname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>Human development</td>
      <td>Ethiopia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11</td>
      <td></td>
      <td>Ethiopia</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Economic management</td>
      <td>Tunisia</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>Social protection and risk management</td>
      <td>Tunisia</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Trade and integration</td>
      <td>Tuvalu</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Test value_counts provide an equivalent result
json_df.countryshortname.value_counts()[:10]
```




    Indonesia             56
    India                 51
    Vietnam               43
    Brazil                41
    Bangladesh            41
    China                 40
    Africa                39
    Yemen, Republic of    34
    Morocco               32
    Mozambique            31
    Name: countryshortname, dtype: int64




```python
# Find top 10 countries
top_10_countries = json_df.groupby('countryshortname')[['code']].count()

top_10_countries.sort_values(by=['code'], inplace=True, ascending=False)

top_10_countries[:10]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>code</th>
    </tr>
    <tr>
      <th>countryshortname</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Indonesia</th>
      <td>56</td>
    </tr>
    <tr>
      <th>India</th>
      <td>51</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>43</td>
    </tr>
    <tr>
      <th>Bangladesh</th>
      <td>41</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>41</td>
    </tr>
    <tr>
      <th>China</th>
      <td>40</td>
    </tr>
    <tr>
      <th>Africa</th>
      <td>39</td>
    </tr>
    <tr>
      <th>Yemen, Republic of</th>
      <td>34</td>
    </tr>
    <tr>
      <th>Morocco</th>
      <td>32</td>
    </tr>
    <tr>
      <th>Mozambique</th>
      <td>31</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Find top 10 projects
top_10_projects = json_df.groupby('code')[['name']].count()

top_10_projects.sort_values(by=['name'], inplace=True, ascending=False)
top_10_projects[:10]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
    </tr>
    <tr>
      <th>code</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>250</td>
    </tr>
    <tr>
      <th>10</th>
      <td>216</td>
    </tr>
    <tr>
      <th>8</th>
      <td>210</td>
    </tr>
    <tr>
      <th>2</th>
      <td>199</td>
    </tr>
    <tr>
      <th>6</th>
      <td>168</td>
    </tr>
    <tr>
      <th>4</th>
      <td>146</td>
    </tr>
    <tr>
      <th>7</th>
      <td>130</td>
    </tr>
    <tr>
      <th>5</th>
      <td>77</td>
    </tr>
    <tr>
      <th>9</th>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Match code with non empty names
fill_not_name = json_df.groupby(['code','name']).count()
fill_not_name.reset_index(inplace=True)

# Remove empty rows
final_filter_filled = fill_not_name[fill_not_name['name'] != '']
final_filter_filled
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>code</th>
      <th>name</th>
      <th>countryshortname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Economic management</td>
      <td>33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10</td>
      <td>Rural development</td>
      <td>202</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>Environment and natural resources management</td>
      <td>223</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Public sector governance</td>
      <td>184</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
      <td>Rule of law</td>
      <td>12</td>
    </tr>
    <tr>
      <th>11</th>
      <td>4</td>
      <td>Financial and private sector development</td>
      <td>130</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5</td>
      <td>Trade and integration</td>
      <td>72</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6</td>
      <td>Social protection and risk management</td>
      <td>158</td>
    </tr>
    <tr>
      <th>17</th>
      <td>7</td>
      <td>Social dev/gender/inclusion</td>
      <td>119</td>
    </tr>
    <tr>
      <th>19</th>
      <td>8</td>
      <td>Human development</td>
      <td>197</td>
    </tr>
    <tr>
      <th>21</th>
      <td>9</td>
      <td>Urban development</td>
      <td>47</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Correct initial DF
json_df_filled = json_df[['code', 'countryshortname']].merge(final_filter_filled[['name', 'code']], on='code')
json_df_filled.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>code</th>
      <th>countryshortname</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>Ethiopia</td>
      <td>Human development</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>China</td>
      <td>Human development</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>Madagascar</td>
      <td>Human development</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>Cambodia</td>
      <td>Human development</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>Cambodia</td>
      <td>Human development</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group by and confirm results
top_10_projects_filled = json_df_filled.groupby('code')[['name']].count()

top_10_projects_filled.sort_values(by=['name'], inplace=True, ascending=False)
top_10_projects_filled[:10]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
    </tr>
    <tr>
      <th>code</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>250</td>
    </tr>
    <tr>
      <th>10</th>
      <td>216</td>
    </tr>
    <tr>
      <th>8</th>
      <td>210</td>
    </tr>
    <tr>
      <th>2</th>
      <td>199</td>
    </tr>
    <tr>
      <th>6</th>
      <td>168</td>
    </tr>
    <tr>
      <th>4</th>
      <td>146</td>
    </tr>
    <tr>
      <th>7</th>
      <td>130</td>
    </tr>
    <tr>
      <th>5</th>
      <td>77</td>
    </tr>
    <tr>
      <th>9</th>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Is corrected DF equivalent to the first result?
top_10_projects_filled.equals(top_10_projects)
```




    True


