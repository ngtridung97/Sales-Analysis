Suppose you were running an Online Electronic site and you need to get some insights from 2019 monthly sales reports. Main idea of the project is coming from this [video](https://www.youtube.com/watch?v=eMOA1pPVUc4&t=4176s).

**Features:**
+ Dataset: [Sample Folder](https://github.com/ngtridung97/Sales-Analysis/tree/master/Sales%20Data%20Examples)
+ Sample Notebook: [Data_Analysis.ipynb](https://github.com/ngtridung97/Sales-Analysis/blob/master/Data_Analysis.ipynb)
+ Sample Period: Calendar Year 2019

See how it works below

### Generate data
----------
The sample dataset is randomly added by this [script](https://github.com/ngtridung97/Sales-Analysis/blob/master/Data_Generate.ipynb). We can adjust the weight of each element to get different versions.

**Data format**
```python
# Data header
columns = ['Order ID', 'Product', 'Quantity', 'Price', 'Order Date', 'Purchase Address']

# Location
street_names = ['1st', ' 2nd', '3rd', '4th', '5th', '6th', '7th', '8th', '9th', '10th', '11th', '12th', '13th', '14th', '15th', '16th', '17th', '18th', '19th', '20th', '21st', '22nd', '23rd', '24th', '25th']
districts = ['01', '02', '03', '04', '05', '06', '07', '08', '10', '11']
districts_weights = [9, 3, 4, 3, 5, 2, 6, 0.5, 3, 1]  

# Product (Price and Frequency)
products = {
  'iPhone': [700, 10],
  'Google Phone': [600, 3],
  'Samsung Phone': [500, 8],
  '21in Monitor': [110, 6],
  '27in Monitor': [150, 11],
  '34in 2k Monitor': [380, 9],
  '27in 4K Gaming Monitor': [400, 9],
  'Dell Laptop': [800, 7],
  'ThinkPad Laptop': [1000, 6],
  'Macbook Pro Laptop': [1700, 7],
  'Power Bank': [60, 30],
  'USB-C Charging Cable': [12, 30],
  'Lightning Charging Cable': [15, 30],
  'Normal Headphones': [12, 30],
  'Sony Headphones': [100, 19],
  'Airpods Headphones': [150, 15]
  }
```
**Result**

![](https://github.com/ngtridung97/Sales-Analysis/blob/master/Image/1.png?raw=true)

### Analyze data
----------
The sample analysis file is performed by this [script](https://github.com/ngtridung97/Sales-Analysis/blob/master/Data_Analysis.ipynb).

**Concatenate csv files**
```python
os.chdir("./Sales Data Examples")
extension = 'csv'
all_filenames = [i for i in glob.glob('*.{}'.format(extension), recursive=True)]
combined_csv = pd.concat([pd.read_csv(f) for f in all_filenames])
combined_csv.to_csv( "Sales_2019.csv", index=False, encoding='utf-8-sig')
```
**Clear outliers**
```python
sales = sales.dropna(how='all')
sales = sales[sales['Order Date'].str[0:4] != 'Null']
```
**Sales by Month**

![](https://github.com/ngtridung97/Sales-Analysis/blob/master/Image/2.png?raw=true)

**Sales by Territory**

![](https://github.com/ngtridung97/Sales-Analysis/blob/master/Image/3.png?raw=true)

**Top 5 bundles**
```python
sales = sales.dropna(how='all')
sales = sales[sales['Order Date'].str[0:4] != 'Null']

from itertools import combinations
from collections import Counter

count = Counter()

for row in df_pair['Bundle']:
    row_list = row.split(', ')
    count.update(Counter(combinations(row_list, 3)))

for key, value in count.most_common(5):
    print(key, '-', value, 'times')
```

![](https://github.com/ngtridung97/Sales-Analysis/blob/master/Image/4.png?raw=true)

### Feedback & Suggestions
----------
Please feel free to fork, comment or give feedback to ng.tridung97@gmail.com