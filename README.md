# Cubic Spline
Created for use in the project [Electricity-Demand-Prediction](https://github.com/Ishan5hrestha/Electricity-Demand-Prediction).  
The electric data obtained from Nepal Electricity Authority(NEA) had some fields missing, mainly due to cutting off of power for maintainence purposes or data being unreadable. These values had to be recovered for proper training of model. Hence, the use of **cubic spline**
## cubic_spline()
The function takes two arguments, x-axis values & y-axis values.  
- X-axis values are serial values of the base axis, in our case, time of the day
- Y-axis values are the data corresponding to the X-axis value with some of them missing, in our case, electric load data

The missing values are written as 0. The function is programmed to replace those 0s with interpolated values.
Both these values are in form of a list and the output list is the Y-axis list with all recovered values.

## interpollable()
Cubic spline uses all the values to calculate the values. If subsequent values are missing, the interpolation gives quite different value than the actual missing values. Hence in such case where 2 subsequent values are missing, the interpollable returns False ie. it can't/mustn't be interpolated directy.  
Otherwise it returns True, then the data is passed into cubic_spline() function.

averager and interpollable are extra bits not needed for interpolation.  
They are basically used to get data from previous lines of data in case multiple consecutive values are missing which makes interpolating very inaccurate.  
averager  
 -checks previous and next row for data and adds average of them to alternating places where data is missing  
 -mylist0 takes y-axis values of beforehand row  
 -mylist takes y-axis value of the row we need to interpolate  
 -mylist1 takes y-axis values of following row  
 -returns the value restored list  
    
interpollable just checks if there are consecutive values missing and returns true or false
