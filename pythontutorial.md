```python



from aguaclara.core.units import unit_registry as u
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats
data_file_path = "dataforpythontutorial.txt"

df = pd.read_csv(data_file_path,delimiter='\t')

#if you want to see what is in the dataframe you can print it!
print(df)
# The column headers can be access by using the list command
list(df)
columns = df.columns
print(columns)
#Below are three equally fine methods of extracting a column of data from the pandas dataframe.
# 3) We can use the iloc command and select all of the rows in column 0.
x = df.iloc[:,0].values * u.mm
x
y = df.iloc[:,1].values * u.mm
y
# We will use the stats package to do the linear regression.
 # It is important to note that the units are stripped from the x and y arrays when processed by the stats package.
slope, intercept, r_value, p_value, std_err = stats.linregress(x,y)
slope
y.units

#We can add the units to intercept by giving it the same units as the y values.
intercept

# For the general case we can attach the correct units to slope.
intercept = intercept * y.units
intercept
slope = slope * y.units/x.units
# Now create a figure and plot the data and the line from the linear regression.
slope
fig, ax = plt.subplots()
ax.plot(x, y, 'ro', )
#plot the linear regression as a black line
ax.plot(x, slope * x + intercept, 'k-', )

# Add axis labels using the column labels from the dataframe
ax.set(xlabel=list(df)[0])
ax.set(ylabel=list(df)[1])
ax.legend(['Measured', 'Linear regression'])
ax.grid(True)
# Here I save the file to my local harddrive. You will need to change this to work on your computer.
# We don't need the file type (png) here.

plt.savefig('~/Documents/github/4530-aks224')


plt.show()
```
![plot](
        http://github.com/AnyaSherman/4530-aks224//blob/master/figure.png)
      )
