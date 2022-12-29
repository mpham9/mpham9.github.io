---
layout: page
title: "My notes"
permalink: /notes/
published: false
---

# Setup

Set up virtual environment
```
python -m venv path\to\virtualenvironment
```
Activate virtual environment
```
.\env\Scripts\activate
where python
```
Leaving virtual environment
```
deactivate
```
Install packages
```
python -m pip install plotly
python -m pip install requests==2.18.4
```
Freeze dependencies
```
python -m pip freeze
```



# Data wrangling

Pandas axis:
- '0' : index or row
- '1' : column

Insert column into Pandas dataframe
```Python
df.insert(loc: 'int', column: 'str|number|hashable', value: 'scalar|serires|array-like', allow_duplicates: 'bool'=False)
df.insert(5,'Scenario','')
```

Extract table from PDF file
```Python
import tabula
df = tabula.read_pdf('filename.pdf',pages=2)
df.to_excel('filename_p2.xlsx')
```

Extract number using pattern
```Python
import re
filename = "filename.lp"
regex = '(?<=\\+\\s)[0-9\\.]+(?=\\sConVio_N1_BuildLimit)'
match_list = []
with open(filename, "r") as file:
    for line in file:
        for match in re.finditer(regex, line):
            match_text = match.group()
            match_list.append(match_text)
            print(line)           
len([float(i) for i in match_list if float(i) != 0])
sum([float(i) for i in match_list])
```

Exception handling
```Python
def log_deriv(x,e):
  try:
    return (math.log(x+e)-math.log(x))/e
  except (ValueError, TypeError):
    return None
y = log_deriv(-1,0)

f = open(path, mode="w")
try:
    write_to_file(f)
finally:
    f.close() # always execute regardless of whether or not the try block succeeds
    
f = open(path,mode="w")
try:
    write_to_file(f)
except:
    print("Failed")
else:
    print("Succeeded") # executes only if the try block succeeds using else
finally:
    f.close()
    
    
```

Array creation
```Python
import numpy as np
# array of zeros
np.zeros(5)
np.zeros((2,3))

# diagonal matrix
np.eye(4)

# array with ones
np.ones((5,2))

# array filled with specified value
np.full((4,3), True)

# empty array
np.empty((4,))

# equally spaced grid
np.linspace(1.0,8.0,5)
```

Copy to new variables (otherwise new variables point to the same Python object)
```Python
import numpy as np
a = np.array([[1,2],[3,4]])
b = np.zeros(a.shape)
b[:,:] = a
# or alternatively
np.copyto(b,a)
```

Get data 
```Python
# for index value 50
df.loc[5]
# for index values from 0 to 5
df.loc[0:5]
# for rows in positions in range 0 to 5
df.iloc[0:5]
# for row 0, columns in positions 1 and 2
df.iloc[0,[1,2]]
# 
df.loc[0,'Grade']
#
df.loc[df['Name']=='Aisha']
df[df['Name']=='Aisha']
# 
df.query('Name=="Aisha"')
# 
df[df.Name == 'Aisha']
#
df[df.columns[0:6]]
```

Check null
```Python
df.isnull()
df[df.isnull().any(axis=1)]
```

Drop na
```Python
# axis = 0: Drop rows having na values, axis = 1: drop columns
df = df.dropna(axis=0,how='any')
```

Filter
```Python
df[df.StudyHours > mean_study]['StudyHours']
```

Combine columns
```Python
a = pandas.concat([b,c],axis=1)
```

Group by
```Python
print(df.groupby(df.Pass).Name.count())
print(df.groupby(df.Pass)['StudyHours','Grade'].mean())
a = df.groupby(['Year','Month','Day']).sum(numeric_only=True)
```

Sort
```Python
df = df.sort_values('Grade',ascending=False)
df = df.sort_values(by = ['Year','Month','Day'])
```

Bar plot
```Python
from matplotlib import pyplot as plt
plt.bar(x=df.Name, height=df.Grade)
plt.title('Student Grades')
plt.xlabel('Student')
plt.xticks(rotation=90) # vertical texts on x axis
plt.show()
```

Column chart
```Python
df.plot(x='Name',y=['Grade','StudyHours'],kind='bar',figsize=(8,5))
```

Subplot
```Python
fig, ax = plt.subplots(1,2,figsize=(10,4))
ax[0].bar(x=df.Name,height=df.Grade,color='orange')
ax[0].set_title('Grades')
ax[0].set_xticklabels(df.Name,rotation=90)
pass_count = df['Pass'].value_counts()
ax[1].pie(pass_count,labels=pass_counts)
ax[1].legend(pass_counts.keys().tolist())
fig.suptitle('Student Data')
fig.show()
```

Add vertical line
```Python
plt.hist(var)
plt.axvline(x=med_val, color='red',linestyle='dashed',linewidth=2)
```

Plot density
```Python
fig = plt.figure(figsize=(10,4))
df.plt.density()
plt.show()
```

Quantile
```Python
q01 = df.StudyHours.quantile(0.01)
```

Get day
```Python
df['day'] = pandas.DatetimeIndex(df['date']).day
```

Train model
```Python
X_train, X_test, y_train, y_test = sklearn.model_selection.train_test_split.train_test_split(X,y,test_size=0.3)
model = sklearn.linear_model.LinearRegression.LinearRegression().fit(X_train,y_train)
prediction = model.predict(X_test)
```

Subtract all rows of data frame by a row
```Python
df.sub(df.iloc[1],axis=1)
df.sub(df["col2"],axis=0)
```

Plotly in Spyder
```Python
import plotly.io as pio
pio.renderers.default='browser'
```

Moving average, rolling sum
```Python
df['SMA14'] = df['daily_rating'].rolling(window=14).mean()
df = df.dropna(axis=0)
```

Filter min max
```Python
df[df.rating == df.rating.min()]
```

Apply conditional new column
```Python
df['fy'] = df.apply(lambda x: x['Year'] if x['Month'] < 7 else x['Year'] + 1, axis = 1)
```

Left join
```Python
res = pandas.merge(df1,df2,how='left',left_on=['col1','col2'],right_on=['colA','colB'])
```

weighted average
```Python
res['prod'] = res['weights'] * res['values']
res = df.groupby('fy').sum()
res['weighted'] = res['prod'] / res['weights']
```

String format
```Python
#{0:.2f} means first argument as floating-point number with 2 decimal places
#{1:s} means second argument as string
#{2:d} means third argument as exact integer

"{0:.2f} {1:s} are worth US${2:d}".format(88,"Argentine Pesos",1)

amount = 10
rate = 88
currency = "Pesos"
res = f"{amount} {currency} is worth US${amount /rate:.2f}"
```

Use `r` for no escape character
```Python
s = r"this\has\no\special\characters"
```

if,elif,else
```Python
if x<0:
    # do something
elif x==0 or c>d:
    # do something
elif 0<x<5:
    # do something
else:
    # do something
```

for loop, continue, break
continue: skip the remainder of the block, advancing a for loop to the next iteration
break: terminate the innermost for loop, any outer for loops will continue to run
```Python
for value in collection:
    if value is None:
        continue
    total += value
    
for i in range(3):
    for j in range(5):
        if j>i:
            break
        print((i,j))
```

Long to wide
```Python
df = df.pivot(index=["date","time"],columns="variable",values="value").reset_index()

df = df.set_index(["date","time"]).unstack(level="item")
df = df.unstack() # inner most level is unstack first
df = df.unstack(level=0)
df = df.unstack(level="state")
```

Wide to long
```Python
df = df.stack().reset_index().rename(columns={0:"value"})

df = df.melt(id_vars="key",value_vars=["A","B"])
```
