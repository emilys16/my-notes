---
title: The Book of Negroes - Python Exercise 2
draft: false
tags:
  - CTS2000
---
___
# Step 0: Import the pandas library and load the CSV file into the dataframe
```python
#Import the necessary libraries to do our file input / output
#Import Pandas to work with the data files 
import os
%pip install pandas
import pandas as pd

#Load the datasets
BoN = pd.read_csv("Book_of_Negroes.csv")
BoN_Expanded = pd.read_csv("Book_of_Negroes_expanded.csv",header=None)

# CLEANING THE EXPANDED DATA
# Rename the columns
BoN_Expanded.columns = ['Name', 'Age', 'Description']
# Drop rows where all columns are NaN
BoN_clean = BoN_Expanded.dropna(how='all')
def clean_hidden_characters(text):
    if isinstance(text, str):  # A Boolean that checks if the value is a string; it takes two parameters: the object to be checked and the type (eg. str, int, etc)
        # Remove leading/trailing whitespace and replace unicode \xao
        return text.strip().replace(u'\xa0', u' ')
    return text  # Returns text, leaving NaN or nonstring columns unchanged

# Apply the cleaning function to the 'Description' column and reassign it
BoN_clean.loc[:, 'Description'] = BoN_clean['Description'].apply(clean_hidden_characters)
```

# Step 1: Aggregate the data from two tables

In step 1, we created a copy of the DataFrame and using Pandas identified people that appear in both datasets. We used the merge() function to aggregate the BoN_new and BoN_Expended into one chart. 

```python
# Create a copy of the dataset 
BoN_new = BoN.copy()

#Aggregated the data from the two tables 
merged_df = pd.merge(BoN_new, BoN_Expanded, left_on='ARname', right_on='Name', how='inner')

# Display the result
merged_df
```

# Step 2: Research Question 
The research question I chose to analyze was: What points of origin are mentioned in the descriptions recorded in the Book?

The description column contains information on place of origin, health, physical traits, slave owner's name, family members, and certification. 

# Step 3: Creating a pattern match
```python
pd.set_option('display.max_rows', None)  # Shows all rows
pd.set_option('display.max_columns', None)  # Shows all columns
pd.set_option('display.max_colwidth', None)  # Full content of each column cell

# Extract points of origin using Pandas' str.extract with a regex pattern to extract points of origins
#captures locations with at least three characters that start with a capital letter, treating them as proper nouns
#Ensure regex statement captures points of origin prefixed by "of" but excludes those specifically prefixed by "property of"

merged_df['points_of_origin'] = merged_df['Description'].str.extract(r'(?<!property\s)(?:from|lived in|of|freeborn on|freeborn in)\s+([A-Z][a-zA-Z\s]{3,})',expand=False)

# Drop rows with NaN values in point_of_origin column
points_of_origin = merged_df['points_of_origin'].dropna()

# Count occurrences of each point of origin
origin_counts = points_of_origin.value_counts()

if not origin_counts.empty:
    print("Points of Origin and their counts:\n", origin_counts)
else:
    print("No origins found")
```

# Step 4: Analyzing the data
```python
# Used panda plot to create a data visualization 
merged_df['points_of_origin'].value_counts().plot(kind='pie', figsize=(20,5), title='The Book of Negroes:\norigin recorded in the Book')
```

```python
# Used panda plot to create a data visualization 
merged_df['points_of_origin'].value_counts().plot(kind='area', figsize=(20,5), title='The Book of Negroes:\norigin recorded in the Book')
```

### What are the most common results?
The most common result from the data anlaysis are River St, Charlestwon South Carolina, Norfolk Virginia as shown in the pie chart. 
### What are the least common or outliers?
The least common origin points from the data analysis are Virginia, Guin, and Fairefield as shown in the area chart. 
### Compare and close read an individual example of a typical result with one that is atypical (unusual, an outlier). What do you notice or observe?
A specific example is the data on Guin which is a city in Alabama. It is atypical as shown in the area chart by being on the right side of the chart closer to zero. They may be because the majority of people are coming from the coast line while Guin is landlocked. 

# Step 5: Reflection

## Topic: Points of origin in the Book of Negroes

### Historical Context
- The Book of Negroes is a historical document that lists Black loyalists who were evacuated to Nova Scotia from the New York after the American Revolutionary War (Ncurrie).

- The document contains detailed information, including the names, genders, ages, and physical descriptions of individuals, along with details regarding their escape, military service records, the names and destinations of the ships they boarded, and their dates of departure (Hill). Additionally, when relevant, it notes the names of former or current White slave masters associated with these individuals (Hill).

### Geographical Locations
- Some people mentioned in the Book of Negroes were born in various regions of Africa, especially West Africa, which was highly involved in the transatlantic slave trade. Most of the people mentioned in the Book of Negroes were born to parents that were already slaves in the American colonies where slavery was practiced, such as Virginia, Maryland, and South Carolina (Nova Scotia Archives)

### Limitations of Analysis and Further Questions
- One particular limitation of analysis was being able to write a code that excluded some words based on the context they were used. For example, some people's origins were written as "[name] of [location]." In this case, we could use the word "of" to capture their data. In other cases, the word "of" indicated ownership (i.e. Property of [slavemaster name]). This made it very difficult to ensure that the parameters we were setting in the regex statement would include and exclude the correct data.

- Another limitation of analysis was incomplete data entries. Some columns in the dataset were left empty. In the case of geographical locations, not every person's description included a place of origin. This lack of uniformity can skew the analysis of the data and cause an underrepresentation of certain demographics.
  
- One lingering question we have is about data enrichment. Are there other datasets available that could complement the "Book of Negroes"? For instance, census data, personal letters, or other historical records that provide more context to the lives of these individuals?

## References

Hill, Lawrence. “Behind the Book of Negroes - Canada’s History.” Canadashistory.ca, 10 Feb. 2015, www.canadashistory.ca/explore/books/behind-the-book-of-negroes. Accessed 20 Oct. 2024.

Ncurrie. “Record of the Week: The Book of Negroes.” Rediscovering Black History, National Archives, 5 Feb. 2015, rediscovering-black-history.blogs.archives.gov/2015/02/05/rotw-the-book-of-negroes/. Accessed 19 Oct. 2024.

Nova Scotia Archives. “Nova Scotia Archives - African Nova Scotians in the Age of Slavery and Abolition.” Nova Scotia Archives, 20 Apr. 2020, archives.novascotia.ca/africanns/book-of-negroes/.
 
