
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

| brand_name | item_description | count |
| --- | --- | --- |
| NotSet | IsSet | 6032 |
| Nintendo | NotSet | 873 |
| NotSet | NotSet | 674 |
| Sony | NotSet | 461 |
| Xbox | NotSet | 401 |
| Microsoft | NotSet | 13 |

#### Unfiltered

| brand_name | item_description | count |
| --- | --- | --- |
| NotSet | IsSet | 8948 |
| Nintendo | NotSet | 1093 |
| NotSet | NotSet | 896 |
| Sony | NotSet | 553 |
| Xbox | NotSet | 508 |
| Microsoft | NotSet | 22 |


### Verify closest categories
Adding 40% more data with the "Video Game" category token requires the verification of the categories included along. Then, the initial data filters are redefined to retrieve all categories that include "Video Game" and steps above are repeated. 

|  | category_name |
| --- | --- |
| 0 | Electronics/Video Games & Consoles/Consoles |
| 1 | Electronics/Video Games & Consoles/Games |
| 2 | Electronics/Video Games & Consoles/Video Gamin... |
| 3 | Vintage & Collectibles/Electronics/Video Game |
| 4 | Electronics/Video Games & Consoles/Accessories |
| 5 | Electronics/Video Games & Consoles/Other |
| 6 | Electronics/Video Games & Consoles/Strategy Gu... |
| 7 | Electronics/Video Games & Consoles/Replacement... |



### Redo filters
"Video Game" token is identified as an inclusive category which brings 40% more data than "Electronics/Video Games & Consoles/Games", and it is all related items.

|  | brand_name | from category | with token | change |
| --- | --- | --- | --- | --- |
| 0 | Nintendo | 10044 | 14591 | 0.452708 |
| 1 | NotSet | 6706 | 9844 | 0.467939 |
| 2 | Sony | 5381 | 7445 | 0.383572 |
| 3 | Xbox | 4046 | 5656 | 0.397924 |
| 4 | Microsoft | 211 | 514 | 1.436019 |