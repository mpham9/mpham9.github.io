
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
  except ValueError:
    return None

y = log_deriv(-1,0)
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
```

Sort
```Python
df = df.sort_values('Grade',ascending=False)
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
