```python
# prompt: connect to google drive

from google.colab import drive
drive.mount('/content/drive')

```
```
Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).

```
```python
import pandas as pd
import numpy as np
import warnings
import matplotlib as mpl
import matplotlib.pyplot as plt
# Use the fivethirtyeight style
plt.style.use('fivethirtyeight')

mpl.rcParams['figure.figsize'] = (10, 7)
mpl.rcParams['axes.grid'] = True

pd.set_option('display.expand_frame_repr', False)

for cat in [DeprecationWarning, UserWarning, FutureWarning]:
    warnings.filterwarnings("ignore", category=cat)
```
```python
# Read in the file content in a DataFrame called discoveries
discoveries = pd.read_csv('/content/drive/MyDrive/TimesSeries/Week9/Dataset/discoveries.csv')

# Display the first five lines of the DataFrame
print(discoveries.head())
```
```
         date  Y
0  01-01-1860  5
1  01-01-1861  3
2  01-01-1862  0
3  01-01-1863  2
4  01-01-1864  0

```
```python
# Print the data type of each column in discoveries
print(discoveries.dtypes)

# Convert the date column to a datestamp type
discoveries['date'] = pd.to_datetime(discoveries['date'])

# Print the data type of each column in discoveries, again
print(discoveries.dtypes)
```
```
date    object
Y        int64
dtype: object
date    datetime64[ns]
Y                int64
dtype: object

```
# Lets get started
```python
# Set the date column as the index of your DataFrame discoveries
discoveries = discoveries.set_index('date')
```
```python
import seaborn as sns

```
```python
# Plot the data using seaborn
plt.figure(figsize=(10, 6))
sns.lineplot(data=discoveries, x='date', y='Y')
plt.title('Number of Great Inventions and Scientific Discoveries (1860-1959)')
plt.xlabel('Date')
plt.ylabel('Number of Discoveries')
plt.grid(True)
plt.show()

# Plot the time series in your DataFrame
ax = discoveries.plot(color='blue')

# Specify the x-axis label in your plot
ax.set_xlabel('Date')

# Specify the y-axis label in your plot
ax.set_ylabel('Number of great discoveries')

# Show plot
plt.show()
```
```python
# Import the matplotlib.pyplot sub-module
import matplotlib.pyplot as plt

# Use the fivethirtyeight style
plt.style.use('fivethirtyeight')

# Plot the time series
ax1 = discoveries.plot()
ax1.set_title('FiveThirtyEight Style')
plt.show()
```
```python
# Import the matplotlib.pyplot sub-module
import matplotlib.pyplot as plt

# Use the ggplot style
plt.style.use('ggplot')
ax2 = discoveries.plot()

# Set the title
ax2.set_title('ggplot Style')
plt.show()
```
```python
# Plot a line chart of the discoveries DataFrame using the specified arguments
ax = discoveries.plot(color ='blue', figsize=(8, 3), linewidth=2, fontsize=6)

# Specify the title in your plot
ax.set_title('Number of great inventions and scientific discoveries from 1860 to 1959', fontsize=8)

# Show plot
plt.show()
```
```python
# Select the subset of data between 1945 and 1950
discoveries_subset_1 = discoveries['1945':'1950']

# Plot the time series in your DataFrame as a blue area chart
ax = discoveries_subset_1.plot(color='blue', fontsize=15)

# Show plot
plt.show()
```
```python
# Select the subset of data between 1939 and 1958
discoveries_subset_2 = discoveries['1939-01-01':'1958-01-01']

# Plot the time series in your DataFrame as a blue area chart
ax = discoveries_subset_2.plot(color='blue', fontsize=15)

# Show plot
plt.show()
```
```python
# Plot your the discoveries time series
ax = discoveries.plot(color='blue', fontsize=6)

# Add a red vertical line
ax.axvline('1939-01-01', color='red', linestyle='--')

# Add a green horizontal line
ax.axhline(4, color='green', linestyle='--')

plt.show()
```
```python
# Plot your the discoveries time series
ax = discoveries.plot(color='blue', fontsize=6)

# Add a vertical red shaded region
ax.axvspan('1900-01-01', '1915-01-01', color='red', alpha=0.3)

# Add a horizontal green shaded region
ax.axhspan(6, 8, color='green', alpha=0.3)

plt.show()
```
```python
from nbconvert import HTMLExporter
import nbformat

# Load notebook
notebook_path = "/content/drive/MyDrive/TimesSeries/Week9/Code/discoveries.ipynb"
output_html_path = "/content/drive/MyDrive/TimesSeries/Week9/html/discoveries.html"
with open(notebook_path) as f:
    notebook_content = nbformat.read(f, as_version=4)

# Convert to HTML
html_exporter = HTMLExporter()
(body, resources) = html_exporter.from_notebook_node(notebook_content)

# Save to HTML file
with open(output_html_path, "w") as f:
    f.write(body)

```
