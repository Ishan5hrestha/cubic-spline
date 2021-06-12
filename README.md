# cubic-spline
cubic_spline  
    -performs cubic spline  
    -xvals take the data on x-axis  
    -mylist take the data on y-axis  
    -returns back the interpolated list  
  
averager and interpollable are extra bits not needed for interpolation.  
They are basically used to get data from previous lines of data in case multiple consecutive values are missing which makes interpolating very inaccurate.  
averager  
 -checks previous and next row for data and adds average of them to alternating places where data is missing  
 -mylist0 takes y-axis values of beforehand row  
 -mylist takes y-axis value of the row we need to interpolate  
 -mylist1 takes y-axis values of following row  
 -returns the value restored list  
    
interpollable just checks if there are consecutive values missing and returns true or false
