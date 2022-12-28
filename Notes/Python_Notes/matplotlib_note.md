# Matplotlib
Python data visualization library

***

## Contents
1) [Pyplot](#id-1)
2) [Markers](#id-2)
3) [Line](#id-3)
4) [Labels](#id-4)
5) [Grid Lines](#id-5)
6) [Subplot](#id-6)
7) [Scatter Plot](#id-7)
8) [Bar graph](#id-8)
9) [Histograms](#id-9)
10) [Pie Charts](#id-10)


***

<div id="id-1"></div>

### 1) Pyplot

```python
import matplotlib.pyplot as plt
import numpy as np

x_points = np.array([2, 4, 6, 8])
y_points = np.array([1, 10, 5, 8])

plt.plot(x_points, y_points)
plt.show()
```
![pyplot image](/Codes/matplotlib_learnings/images/pyplot_1.png)

***

<div id="id-2"></div>

### 2) Markers

```python
plt.plot(y_points, marker = 'o') 
```

| marker | description           |
|--------|-----------------------|
| 'o'    | 	Circle            |
| '*'    | 	Star	          |
| '.'    | 	Point	          |
| ','    | 	Pixel	          |
| 'x'    | 	X	              |
| 'X'    | 	X (filled)	      |
| '+'    | 	Plus	          |
| 'P'    | 	Plus (filled)	  |
| 's'    | 	Square	          |
| 'D'    | 	Diamond	          |
| 'd'    | 	Diamond (thin)    |
| 'p'    | 	Pentagon	      |
| 'H'    | 	Hexagon	          |
| 'h'    | 	Hexagon	          |
| 'v'    | 	Triangle Down	  |
| '^'    | 	Triangle Up	      |
| '<'    | 	Triangle Left	  |
| '>'    | 	Triangle Right	  |
| '1'    | 	Tri Down	      |
| '2'    | 	Tri Up	          |
| '3'    | 	Tri Left	      |
| '4'    | 	Tri Right         |
| '_'    | 	Hline             |

#### Format String
```python
plt.plot(y_points, 'o:r')
```

* Lines `-` `:` `--` `-.`
* Color `r` `g` `b` `c`(cyan) `m`(magenta) `y`(yellow) `k`(black) `w`(white)

#### Marker Size
```python
plt.plot(y_points, marker = 'o', ms = 20)
```

#### Marker Edge Color

```python
plt.plot(y_points, marker = 'o', ms = 20, mec = 'r')
```

#### Marker face color  (inside edge)
```python
plt.plot(y_points, marker = 'o', ms = 20, mfc = 'r')
```

***

<div id="id-3"></div>

### 3) Line 

* Line style

```python
plt.plot(y_points, linestyle = 'dotted')
#OR
plt.plot(y_points, ls = ':')
```

* Line color

```python
plt.plot(y_points, color = 'r')
#OR
plt.plot(y_points, c = '#4CAF50')
```

* linewidth or lw

```python
plt.plot(ypoints, linewidth = '20.5')
```
#### Plotting multiple lines/graph in same plot
```python
plt.plot(x1, y1)
plt.plot(x2, y2)

#OR

plt.plot(x1, y1, x2, y2)
```

***

<div id="id-4"></div>

### 4) Labels

```python
plt.plot(x, y)

font1 = {'family':'serif','color':'blue','size':20}
font2 = {'family':'serif','color':'darkred','size':15}

plt.title("Speed data", loc = 'left', fontdict = font2)
plt.xlabel("time", fontdict = font2)
plt.ylabel("distance", fontdict = font2)
```
Here, `loc` and `fontdict` are 'OPTIONAL'

***

<div id="id-5"></div>

### 5) Grid Lines

```python
plt.plot(x, y)
plt.grid()   # Adds both axis as default
```

```python
plt.grid(axis = 'x')  # x axis grid only
```

#### Grid line properties

```python
plt.grid(color = 'green', linestyle = '--', linewidth = 0.5)
```

***

<div id="id-6"></div>

### 6) Subplot

```python
# plot 1:
import matplotlib.pyplot as plt

plt.subplot(1, 2, 1)  # 1 row 2 column, first plot
plt.plot(x, y)
plt.title("title of plot 1")

# plot 2:

plt.subplot(1, 2, 2)
plt.plot(x, y)
plt.title("title of plot 2")

plt.suptitle("A single title for entire figure")
plt.show()
```

***

<div id="id-7"></div>

### 7) Scatter Plot

* single plot
```python
x = np.array([8,7,7,7,2,17,7,9,4,13,12,9,6])
y = np.array([89,87,78,88,111,86,73,87,94,113,77,85,86])
plt.scatter(x, y)   # x and y are same length
```

* two plots, by default will have two color

```python
# plot 1 data
plt.scatter(x1, y1)

# plot 2 data
plt.scatter(x2, y2)
```

#### color map

```python
x = np.array([1,2,3,4,5,6,7,8,9,10])
y = np.array([100,50,20,30,10,80,90,70,10,60])
colors = np.array([10, 20, 30, 40, 50, 60, 70, 80, 90, 100])

plt.scatter(x, y, c=colors, cmap='viridis')
plt.colorbar()  # (OPTIONAL) includes color bar also in figure
```

![Scatter plot](/Codes/matplotlib_learnings/images/scatter_plot_1.png)

***

<div id="id-8"></div>

### 8) Bar graph

```python
x = np.array(["A", "B", "C", "D"])
y = np.array([1, 55, 7, 44])

plt.bar(x,y)        # vertical bar (default)
plt.show()
```

* for horizontal bar graph `plt.barh(x, y)`
* bar color, width,height.. can be customised

***

<div id="id-9"></div>

### 9) Histograms
shows number of observations within each given interval.

```python
x = np.random.normal(100, 10, 50)
plt.hist(x)
```

![histogram](/Codes/matplotlib_learnings/images/histogram_plot_1.png)

***

<div id="id-10"></div>

### 10) Pie Charts

```python
y = np.array([50, 25, 12.5, 9.5, 3])
my_labels = ["Python", "Java", "Android", "SQL", "shell"]

plt.pie(y, labels=my_labels, startangle=90)  # default angle is 0
plt.title("My work experience")
```

![pie chart](/Codes/matplotlib_learnings/images/piechart_1.png)

***

Reference: https://www.w3schools.com/python/matplotlib_getting_started.asp