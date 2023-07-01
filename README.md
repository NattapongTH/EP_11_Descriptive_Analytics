# <p align="center"> The Journey into Time Series: Beginning with Descriptive Analytics  </p>
### <p align="center"> Data Mastery Series - Episode 11: The Art of Forecasting (Part 2) </p>

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

**Frequency Distribution Table:**
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

Next, we explore Heat Maps to get a more comprehensive understanding of the data.

**Heat Map:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/13.%20Heatmap.png)

Python code for generating the Heat Maps:
```python 
# Plotly

fig = go.Figure(data=go.Heatmap(z=frequency_df.values,
                               x=frequency_df.columns,
                               y=frequency_df.index,
                               colorscale='YlGnBu'))

fig.update_layout(title="Frequency Analysis by SKU",
                  xaxis=dict(title="SKU"),
                  yaxis=dict(title="Value"), 
                  coloraxis_colorbar=dict(title="Frequency"))

pio.show(fig)
```

Moving forward, we delve into Pie Charts.

** Pie Chart:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/14.Piechart.png)

Python code for generating the Pie Charts:
```python 
# Calculating the sum of values for each SKU
sku_sum = df_pivot.sum()

plt.figure(figsize=(4, 4))  # Adjust the figure size as desired

# Creating the pie chart
plt.pie(sku_sum, labels=sku_sum.index, autopct='%1.1f%%')
plt.title('Pie Chart: Sum of Value by SKU')
plt.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
plt.show()
```

Next, we create Bar Charts to compare data across different categories.

** Bar Chart:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/15.Barchart.png)

Python code for generating the Bar Charts:
```python 
# Extracting the data for the x-axis (sku) and y-axis (sum of value)
x = df_pivot.columns[1:].tolist()  # Exclude the 'date' column
y = df_pivot.sum().tolist()

plt.figure(figsize=(4, 4))  # Adjust the figure size as desired

# Creating the bar chart
plt.bar(x, y)
plt.xlabel('SKU')
plt.ylabel('Sum of Value')
plt.title('Bar Chart: Sum of Value by SKU')
plt.show()
```


And here's another variant of the bar chart:

** Bar Chart-2:**
<br>
![alt](https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/Photo/16.Barchart2.png)

Python code for generating the Bar Chart-2:

```python 
skus = df['sku'].unique()

fig = sp.make_subplots(rows=len(skus), cols=1, shared_xaxes=True, subplot_titles=[f"Frequency analysis for SKU {sku}" for sku in skus], vertical_spacing=0.05)

for i, sku in enumerate(skus):
    frequencies = df[df['sku'] == sku]['value'].value_counts().sort_index()
    fig.add_trace(go.Bar(x=frequencies.index, y=frequencies.values), row=i+1, col=1)

fig.update_layout(height=800, width=500, title_text="Frequency Analysis by SKU")
fig.update_xaxes(title_text="Value", row=len(skus), col=1)
fig.update_yaxes(title_text="Frequency", row=len(skus), col=1)

pio.show(fig)
```