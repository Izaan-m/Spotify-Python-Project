import pandas as pd
import numpy as np
import matplotlib as plt 
import seaborn as sns

from google.colab import drive
drive.mount('/content/drive')
import requests
import pandas as pd

# File ID from your Google Drive link
file_id = '1UCU2rQafKCSqolQLOQFhxf8iOumfkeRU'
new_file_name = 'Spotify.csv'
# Download the file
url = f"https://drive.google.com/uc?id={file_id}"
r = requests.get(url)

# Save the file
with open(new_file_name, 'wb') as f:
    f.write(r.content)

# Load the data
df = pd.read_csv(new_file_name) 


# EDA

# Check the DataFrame Shape
print(df.shape)

print(df.columns)
print(df.columns.tolist())


# View the First Few Rows
print(df.head())


# View the Last Few Rows
print(df.tail())


# Checking DataTypes
print(df.dtypes)

print(df['streams'].dtype)
df['streams'] = pd.to_numeric(df['streams'], errors='coerce')






# # Cleaning the Data:
print(df.isnull().sum())

# # Drop Null Values
df = df.dropna()


# Visualization:
import matplotlib.pyplot as plt
import seaborn as sns  

Total Streams by Year:
# Plotting the histogram for 'streams'
plt.figure(figsize=(10, 6)) 
df['streams'].hist(bins=30)  
plt.title('Distribution of Streams')
plt.xlabel('Streams')
plt.ylabel('Frequency')
plt.grid(False) 
plt.show()



# Box plot for 'danceability_%'
plt.figure(figsize=(10, 6))
sns.boxplot(x='danceability_%', data=df)
plt.title('Box Plot of Danceability')
plt.show()



import matplotlib.pyplot as plt
import seaborn as sns

# Plotting the histogram for 'streams'
plt.figure(figsize=(10, 6))
df['streams'].hist(bins=30, color='skyblue', edgecolor='black')
plt.title('Distribution of Streams')
plt.xlabel('Streams')
plt.ylabel('Frequency')
plt.grid(False)
plt.show()


Total Streams by Released Year:
plt.figure(figsize=(12, 6))
df.groupby('released_year')['streams'].sum().plot(kind='bar', color='purple')
plt.title('Total Streams by Released Year')
plt.xlabel('Released Year')
plt.ylabel('Total Streams')
plt.xticks(rotation=45)
plt.show()


Average Streams by Artist:
# Artist Comparison: Average Streams by Artist
plt.figure(figsize=(12, 6))
df.groupby('artist(s)_name')['streams'].mean().sort_values(ascending=False).head(10).plot(kind='bar', color='teal')
plt.title('Top 10 Artists by Average Streams')
plt.xlabel('Artist Name')
plt.ylabel('Average Streams')
plt.xticks(rotation=45)
plt.show()


Musical Features vs. Streams
# Playlist Appearance
plt.figure(figsize=(12, 6))
df.groupby('in_spotify_playlists')['streams'].mean().plot(kind='bar', color='blue')
plt.title('Average Streams for Spotify Playlist Inclusion')
plt.xlabel('In Spotify Playlists (0 = No, 1 = Yes)')
plt.ylabel('Average Streams')
plt.xticks(rotation=0)
plt.show()


Outlier Detection
# Outliers
plt.figure(figsize=(10, 6))
sns.boxplot(y='streams', data=df)
plt.title('Box Plot of Streams')
plt.ylabel('Streams')
plt.show()


Summary Statistics
print(df.describe())
