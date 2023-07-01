# <p align="center"> The Journey into Time Series: Beginning with Descriptive Analytics  </p>
## <p align="center"> Data Mastery Series - Episode 11: The Art of Forecasting (Part 2) </p>

---

Welcome to my GitHub repository. This section provides a code walkthrough and explanations for the descriptive analytics concepts we've explored in the context of time-series analysis.

**Data source:** 
https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/EP11.xlsx

Sample Dataset:
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/11.%20Dataset.png)

Before we begin, let's set up our environment:

```python 
import numpy as np
import pandas as pd

import seaborn as sns
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.figure_factory as ff
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import plotly.subplots as sp
import plotly.io as pio
```

Our journey starts with the Frequency Distribution Tables.

*** Frequency Distribution Table: ***
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/12.FreqSummaryTable.png)

Python code for generating the Frequency Distribution Tables:
```python 
# Define the SKUs to iterate over
skus = ['A', 'B', 'C']

# Frequency analysis as DataFrames
frequency_dfs = []
for sku in skus:
    sku_df = pd.DataFrame(df[df['sku'] == sku]['value'].value_counts())
    sku_df.columns = [f"Frequency for SKU {sku}"]
    sku_df.sort_index(inplace=True)
    frequency_dfs.append(sku_df)

# Concatenate DataFrames
frequency_df = pd.concat(frequency_dfs, axis=1)
frequency_df.sort_index(inplace=True)

# Fill NaN values with 0
frequency_df.fillna(0, inplace=True)

# Print the frequency DataFrame
frequency_df
```