# <p align="center"> The Journey into Time Series: Beginning with Descriptive Analytics  </p>
## <p align="center"> Data Mastery Series - Episode 11: The Art of Forecasting (Part 2) </p>

---

Welcome to my GitHub repository. This section provides a code walkthrough and explanations for the descriptive analytics concepts we've explored in the context of time-series analysis.

**Data source:** 
https://github.com/NattapongTH/EP_11_Descriptive_Analytics/blob/main/EP11.xlsx

<br>
<br>
<br>
**Sample Dataset:**
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