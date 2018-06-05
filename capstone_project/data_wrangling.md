
# Mercari Price Suggestion Challenge

## Missing values

Flag missing data: Category, description and brand are the fields considered as relevant.

* Rows with missing values could be removed from the dataset, but its volume is significant and cannot be ignored.
* Missing data can be considered as a category itself.

## Outliers

It turns out that videogamers are more dilligent to fill the description for their items, hence the category is considered appropriate to take its data all together.

* There are no patterns in the attributes that could be considered as unsafe for the prospect metrics to be retrieved from the data.

## Steps

### Filter data
Different categories could give heterogeneous patterns for the attributes defined for the tuples. Hence, "Electronics/Video Games & Consoles/Games" is the choosen category for this project, with no specific premises for the selection.

### Flag data
Category, brand and description are initially considered as valuable to further create the models to predict prices. However, there are thousands of records with empty data. Empty data will be flagged as NotSet, which will compund a whole new categorization for the data.

### Review dataset and filters
New insights arised when comparing the current category with the initial unfiltered dataset. Besides the NotSet flag being a 25% of the category dataset, there are items with brands that should be included in the choosen category but fall apart.

#### Initial category
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
      <th></th>
      <th>train_id</th>
    </tr>
    <tr>
      <th>brand_name</th>
      <th>item_description</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NotSet</th>
      <th>IsSet</th>
      <td>6032</td>
    </tr>
    <tr>
      <th>Nintendo</th>
      <th>NotSet</th>
      <td>873</td>
    </tr>
    <tr>
      <th>NotSet</th>
      <th>NotSet</th>
      <td>674</td>
    </tr>
    <tr>
      <th>Sony</th>
      <th>NotSet</th>
      <td>461</td>
    </tr>
    <tr>
      <th>Xbox</th>
      <th>NotSet</th>
      <td>401</td>
    </tr>
    <tr>
      <th>Microsoft</th>
      <th>NotSet</th>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>

#### Unfiltered
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
      <th></th>
      <th>train_id</th>
    </tr>
    <tr>
      <th>brand_name</th>
      <th>item_description</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NotSet</th>
      <th>IsSet</th>
      <td>8948</td>
    </tr>
    <tr>
      <th>Nintendo</th>
      <th>NotSet</th>
      <td>1093</td>
    </tr>
    <tr>
      <th>NotSet</th>
      <th>NotSet</th>
      <td>896</td>
    </tr>
    <tr>
      <th>Sony</th>
      <th>NotSet</th>
      <td>553</td>
    </tr>
    <tr>
      <th>Xbox</th>
      <th>NotSet</th>
      <td>508</td>
    </tr>
    <tr>
      <th>Microsoft</th>
      <th>NotSet</th>
      <td>22</td>
    </tr>
  </tbody>
</table>
</div>


### Verify closest categories
Adding 40% more data with the "Video Game" category token requires the verification of the categories included along. Then, the initial data filters are redefined to retrieve all categories that include "Video Game" and steps above are repeated. 


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
      <th>index</th>
      <th>category_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Electronics/Video Games &amp; Consoles/Consoles</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Electronics/Video Games &amp; Consoles/Games</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Electronics/Video Games &amp; Consoles/Video Gamin...</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Vintage &amp; Collectibles/Electronics/Video Game</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Electronics/Video Games &amp; Consoles/Accessories</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Electronics/Video Games &amp; Consoles/Other</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Electronics/Video Games &amp; Consoles/Strategy Gu...</td>
    </tr>
    <tr>
      <td>7</td>
      <td>Electronics/Video Games &amp; Consoles/Replacement...</td>
    </tr>
  </tbody>
</table>
</div>



### Redo filters
"Video Game" token is identified as an inclusive category which brings 40% more data than "Electronics/Video Games & Consoles/Games", and it is all related items.

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
      <th>brand_name</th>
      <th>train_id_x</th>
      <th>train_id_y</th>
      <th>change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Nintendo</td>
      <td>10044</td>
      <td>14591</td>
      <td>0.452708</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NotSet</td>
      <td>6706</td>
      <td>9844</td>
      <td>0.467939</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sony</td>
      <td>5381</td>
      <td>7445</td>
      <td>0.383572</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Xbox</td>
      <td>4046</td>
      <td>5656</td>
      <td>0.397924</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Microsoft</td>
      <td>211</td>
      <td>514</td>
      <td>1.436019</td>
    </tr>
  </tbody>
</table>
</div>