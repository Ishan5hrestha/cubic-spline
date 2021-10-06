# Cubic Spline
- Created for use in the project [Electricity-Demand-Prediction](https://github.com/Ishan5hrestha/Electricity-Demand-Prediction).  
- The electric data obtained from Nepal Electricity Authority(NEA) had some fields missing, mainly due to cutting off of power for maintainence purposes or data being unreadable. These values had to be recovered for proper training of model. Hence, the use of **cubic spline**
## cubic_spline()
The function takes two arguments, x-axis values & y-axis values.  
- X-axis values are serial values of the base axis, in our case, time of the day
- Y-axis values are the data corresponding to the X-axis value with some of them missing, in our case, electric load data

The missing values are written as 0. The function is programmed to replace those 0s with interpolated values.
Both these values are in form of a list and the output list is the Y-axis list with all recovered values.

## interpollable()
- Cubic spline uses all the values to calculate the values. If subsequent values are missing, the interpolation gives quite different value than the actual missing values. Hence in such case where 2 subsequent values are missing, the interpollable returns False ie. it can't/mustn't be interpolated directy. In this case, data is passed into **averager()** function.  
- Otherwise it returns True, then the data is passed into cubic_spline() function.


For example, lets take these data of 2075-03:
```
Time  : 1	2	3	4	5	6	6.5	7	7.5	8	9	10	11	12	13	14	15	16	17	17.5	18	18.5	19	19.5	20	21	22	23	24
Day 18: 0.8	0.9	0.9	0.9	0.9	1.1	1.1	1.5	4	1.5	1.4	1.5	1.4	0	0	0	0	0	0	0	0	0	0	0	0	0	0	1	0.9

```
Here on day 18, from 12pm, many subsequent values are missing. If we try to interpolate these directly, we r sure to get wrong values.

## averager()
If interpollable returns True, ie. subsequent data is missing, averaging is done with data from pervious day. We can understand this by continuing the previous example:
```
Time  : 1	2	3	4	5	6	6.5	7	7.5	8	9	10	11	12	13	14	15	16	17	17.5	18	18.5	19	19.5	20	21	22	23	24
Day 17: 1	0.9	0	0.9	0.9	1.2	1.3	1.6	1.8	1.8	1.7	1.6	1.6	1.5	1.4	1.4	1.5	1.4	1.5	1.6	1.6	1.6	1.8	1.9	1.9	1.8	1.5	1	0.9
Day 18: 0.8	0.9	0.9	0.9	0.9	1.1	1.1	1.5	4	1.5	1.4	1.5	1.4	0	0	0	0	0	0	0	0	0	0	0	0	0	0	1	0.9
Day 19: 0.9	0.9	0.9	0.9	1	1.1	1.3	1.4	1.5	1.4	1.4	1.4	1.3	1.5	1.4	1.4	1.4	1.4	1.4	1.4	1.4	1.6	1.9	2	2	1.8	1.4	1	0.9

```
The averager just averages the value of upper row and lower row for alternating places. The above data is converted into following as output:

```
Time  : 1	2	3	4	5	6	6.5	7	7.5	8	9	10	11	12	13	14	15	16	17	17.5	18	18.5	19	19.5	20	21	22	23	24
Day 17: 1	0.9	0	0.9	0.9	1.2	1.3	1.6	1.8	1.8	1.7	1.6	1.6	1.5	1.4	1.4	1.5	1.4	1.5	1.6	1.6	1.6	1.8	1.9	1.9	1.8	1.5	1	0.9
Day 18: 0.8	0.9	0.9	0.9	0.9	1.1	1.1	1.5	4	1.5	1.4	1.5	1.4	1.5	0	1.4	0	1.4	0	1.5	0	1.6	0	1.95	0	1.8	0	1	0.9
Day 19: 0.9	0.9	0.9	0.9	1	1.1	1.3	1.4	1.5	1.4	1.4	1.4	1.3	1.5	1.4	1.4	1.4	1.4	1.4	1.4	1.4	1.6	1.9	2	2	1.8	1.4	1	0.9

```
Then this data is finally passed to **cubic_spline()** for interpolation.
## Output
```
Time  : 1	2	3	4	5	6	6.5	7	7.5	8	9	10	11	12	13	14	15	16	17	17.5	18	18.5	19	19.5	20	21	22	23	24
Day 17: 1	0.9	0	0.9	0.9	1.2	1.3	1.6	1.8	1.8	1.7	1.6	1.6	1.5	1.4	1.4	1.5	1.4	1.5	1.6	1.6	1.6	1.8	1.9	1.9	1.8	1.5	1	0.9
Day 18: 0.8	0.9	0.9	0.9	0.9	1.1	1.1	1.5	4	1.5	1.4	1.5	1.4	1.5	1.45	1.4	1.4	1.4	1.45	1.5	1.57	1.6	1.79	1.95	1.9	1.8	1.4	1	0.9
Day 19: 0.9	0.9	0.9	0.9	1	1.1	1.3	1.4	1.5	1.4	1.4	1.4	1.3	1.5	1.4	1.4	1.4	1.4	1.4	1.4	1.4	1.6	1.9	2	2	1.8	1.4	1	0.9

```
The interpolator of the project [Electricity-Demand-Prediction](https://github.com/Ishan5hrestha/Electricity-Demand-Prediction) has few extra features added, namely if there is no previous or next row, the row which is available is copied in alternating in manner.
