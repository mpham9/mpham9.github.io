
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

Get data for index value 5
```
df.loc[5]
```
