## RAINFALL PREDICTION USING LINEAR REGRESSION

### AIM

      TO predict the amount of rainfall in inches using linear regression

### Steps

### 1.Importing the libraries

      Imported libraries such as pandas,numpy.

```
import pandas as pd
import numpy as np
```

### 2.Read the file

```
data=pd.read_csv("austin_weather_final")
```

### 3.Deleting the unnecessary column

```
data=data.drop(["Events","SeaLevelPressureLowInches","Date"],axis=1)
```

### 4.Replacing to numeric values

 Replacing T to trace rainfall with 0 and similarly '-' to 0 because we need numeric values to use in model

 ```
data=data.replace('T',0.0)

data=data.replace('-',0.0)
```

### 5.Save the cleaned data in a new csv file

```
data.to_csv("austin_weather_final.csv")
```

### 6.Import sklearn library

   import sklearn library to perform linear regression and also matplotlib to perform graph

```
import sklearn as sk
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
```

### 7.Read the new csv file

```
data=pd.read_csv("austin_weather_final.csv")
```

### 8.Splitting x and y from the dataset

    here we are going to predict the rainfall using its precipitation column so,we are droping that column from x and storing it in the y.(i.e) x contains input values and y contain output values
    
```
x=data.drop(['PrecipitationSumInches'],axis=1)
y=data["PrecipitationSumInches"]
```

### 9.Reshaping y to 2D array

```
y=y.values.reshape(-1,1)
```

### 10.Storing days in a list

consider a random day for plotting a graph and store all the days in a list named days

```
day_index=798
days=[i for i in range(y.size)]
```
### 11.Initializing Linear regression

```
clf=LinearRegression()
```

### 12.Train the model

```
clf.fit(x,y)
```

### 13.Visualisation
plot a graph between precipitation vs total no. of days
here we are using scatter plot using green for all the days and red for the particular day in the index 798 . And using the filter function to filter all the avg values and stored in a variable x_vis.

```
print("The Precipitation Trend Graph")
plt.scatter(days,y,color='g')
plt.scatter(days[day_index],y[day_index],color='r')
plt.title("Precipitation level")
plt.xlabel("Days")
plt.ylabel("precipitation in inches")
plt.show()
x_vis=x.filter(['TempAvgF','DewPointAvgF','HumidityAvgPercent','SeaLevelPressureAvgInches','VisibilityAvgMiles','WindAvgMPH'])
```

plot a  graph between precipitation and attributes. created Create a subplot grid (3 rows, 2 columns, position i+1) inside for loop of ranfe contains no of columns in x_vis.And using scatter plot to predict the trend.

   
```
print("The precipitation vs attribute trend graph")
for i in range(x_vis.columns.size):
    plt.subplot(3,2,i+1)
    plt.scatter(days,x_vis[x_vis.columns.values[i][:100]],color='g')
    plt.scatter(days[day_index],x_vis[x_vis.columns.values[i]][day_index], color = 'r')
    plt.title(x_vis.columns.values[i])
plt.show()
```

### 14.Conclusion

   Rainfall is expected when the temperature is high and humidity is high.
