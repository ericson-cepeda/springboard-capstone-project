
# Mercari Price Suggestion Challenge

It can be hard to know how much something’s really worth. Small details can mean big differences in pricing. For example, one of these sweaters cost $335 and the other cost $9.99. Can you guess which one’s which?

## Problem

Product pricing gets even harder at scale, considering just how many products are sold online. Clothing has strong seasonal pricing trends and is heavily influenced by brand names, while electronics have fluctuating prices based on product specs.

## Utility

Mercari, Japan’s biggest community-powered shopping app, knows this problem deeply. They’d like to offer pricing suggestions to sellers, but this is tough because their sellers are enabled to put just about anything, or any bundle of things, on Mercari's marketplace.

## Data

**train.tsv, test.tsv**
The files consist of a list of product listings. These files are tab-delimited.

* **train_id or test_id** - the id of the listing
* **name** - the title of the listing. Note that we have cleaned the data to remove text that look like prices (e.g. $20) to avoid leakage. These removed prices are represented as [rm]
item_condition_id - the condition of the items provided by the seller
* **category_name** - category of the listing
* **brand_name**
* **price** - the price that the item was sold for. This is the target variable that you will predict. The unit is USD. This column doesn't exist in test.tsv since that is what you will predict.
* **shipping** - 1 if shipping fee is paid by seller and 0 by buyer
* **item_description** - the full description of the item. Note that we have cleaned the data to remove text that look like prices (e.g. $20) to avoid leakage. These removed prices are represented as [rm]

## Approach

1. Extract the data.
1. Analyse how variables behave with the raw data.
1. Check for missing values and clean the data.
1. Analyse and create new features for the fields name and description.
1. Build models...
1. Train relevant models.
1. Verify resutls.

### Deliverables

1. **Source Code** - iPynb on GitHub.
1. Final report.
1. Slide Deck.
1. Blog post on how this problem was approached.
