# SYED SAIF SYED GHOUSE
# 212224230286

# Exp - 2 Netflix Shows & Movies

## Aim

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

## Procedure / Algorithm

1)Load dataset (netflix_titles.csv).

2)Count movies vs TV shows.

3)Group by country → top contributors.

4)Create pivot table (release year vs type).

5)Visualize with bar & line charts.

## Program

### Load dataset directly from GitHub

```python 
import pandas as pd
import numpy as np

url="https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv"
df=pd.read_csv(url)
print("SYED SAIF SYED GHOUSE")
print("212224230286\n")

print("Shape:",df.shape)

print("Columns:",df.columns,"\n")

print("Types:",df['type'].value_counts(),"\n")
```

### Clean 'date_added' and extract year/month

```python
df['date_added']=df['date_added'].astype(str).str.strip()
df['date_added']=pd.to_datetime(df['date_added'],errors='coerce')
df['year_added']=df['date_added'].dt.year.astype('Int64')
df['month_added']=df['date_added'].dt.month_name()
print("SYED SAIF SYED GHOUSE")
print("212224230286\n")

df.head()
```
###  Movies vs TV Shows
```python
count_by_type = df.groupby('type')['title'].count()
print("SYED SAIF SYED GHOUSE")
print("212224230286\n")
print("Count by Type:\n", count_by_type, "\n")
```
###  Country vs Type Pivot Table
```python
pivot_country_type = df.pivot_table(
index='country',
columns='type',
values='title',
aggfunc='count',
fill_value=0
)

pivot_country_type['Total'] = pivot_country_type.sum(axis=1)
max_country = pivot_country_type['Total'].idxmax()  # country with most titles
max_count = pivot_country_type['Total'].max()
print("SYED SAIF SYED GHOUSE")
print("212224230286\n")
# number of titles
print("Pivot Table (Country vs Type):\n", pivot_country_type.head(), "\n")
print(f"Largest Overall: {max_country} with {max_count} titles\n")
```
### Top 5 Directors
```python
top_directors = df['director'].value_counts().head(5)
print("SYED SAIF SYED GHOUSE")
print("212224230286\n")
print("Top 5 Directors:\n", top_directors, "\n")
```

### Yearly Trend of Additions (Movies vs TV Shows)
```python
trend=df.groupby(['year_added','type']).size().unstack(fill_value=0)
print("SYED SAIF SYED GHOUSE")
print("212224230286\n")
print("Yearly Trend by Type\n")
print(trend.head())
```

### Expand Genres
``` python
df_genre = (
df[['show_id','listed_in']]
.dropna()
.assign(listed_in=df['listed_in'].str.split(', '))
.explode('listed_in')
)

df_expanded = df.merge(df_genre, on='show_id', how='left')

print("SYED SAIF SYED GHOUSE")
print("212224230286\n")

print("Columns after merge:\n", df_expanded.columns)

print("\nExpanded Genre Sample:\n",
df_expanded[['title','listed_in_y']].head())

top_genres = df_expanded['listed_in_y'].value_counts().head(5)
print("\nTop 5 Genres:\n", top_genres, "\n")
```
## Ouptut

### Load dataset directly from GitHub

<img width="951" height="391" alt="Screenshot 2026-02-09 210004" src="https://github.com/user-attachments/assets/c3b87652-486f-4739-bf37-75d5a7c656d4" />

<img width="953" height="635" alt="Screenshot 2026-02-09 210024" src="https://github.com/user-attachments/assets/41558355-4093-4be5-a1a0-7a44562a9977" />

### Clean 'date_added' and extract year/month

<img width="948" height="638" alt="Screenshot 2026-02-09 210236" src="https://github.com/user-attachments/assets/43fcfd7c-df7a-4f9e-b232-d6e3dd939489" />

###  Movies vs TV Shows

<img width="954" height="210" alt="Screenshot 2026-02-09 210311" src="https://github.com/user-attachments/assets/9f143380-d06e-4b5b-b897-4defb420dbfe" />

###  Country vs Type Pivot Table

<img width="953" height="484" alt="Screenshot 2026-02-09 210423" src="https://github.com/user-attachments/assets/79f06edc-e94d-4897-bc66-f517794b225d" />

### Top 5 Directors

<img width="947" height="247" alt="Screenshot 2026-02-09 210450" src="https://github.com/user-attachments/assets/4cf272ab-1834-49fd-a935-0fd0ce7823a2" />

### Yearly Trend of Additions (Movies vs TV Shows)

<img width="948" height="281" alt="Screenshot 2026-02-09 210621" src="https://github.com/user-attachments/assets/4c69c084-ef78-4ed2-bcd3-ae5f8e484632" />

### Expand Genres

<img width="949" height="679" alt="Screenshot 2026-02-09 210655" src="https://github.com/user-attachments/assets/230a86ec-5e26-4a25-84d8-bbc8f5adb093" />


## Result 
Helps Netflix in content planning & investments.
