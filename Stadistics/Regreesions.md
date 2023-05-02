# Lineal

$$ Y = a + bX $$

```chart
type: line
labels: [1,2,3,4,5]
series:
  - title: 
    data: [1,2,3,4,5]
tension: 0.2
width: 80%
labelColors: false
fill: false
```

$$
	b= {\sum(x-\bar{x})(y-\bar{y}) \over \sum(x-\bar{x})^2}
$$

$$
 a = \bar{Y} - b \bar{X}
$$

$$
 R^2 = {\sum (Y_p - \bar{Y})^2 \over \sum (Y - \bar{Y})^2}
$$
# Parabolic
$$
 Y = a+bX+cX^2
$$
```chart
type: line
labels: [1,2,3,4,5]
series:
  - title: 
    data: [5,3,1,3,5]
tension: 0.2
width: 60%
labelColors: false
fill: false
```

# Exponential
$$
 Y = a e^{bX}
$$
```chart
type: line
labels: [1,2,3,4,5]
series:
  - title: 
    data: [1,10,20,50,100]
tension: 0.2
width: 60%
labelColors: false
fill: false
```
$$
 ln{Y} = ln{a} + bX 
$$
$$
Y' = a' + bX
$$
$$
b= {n \sum{XY'}-\sum{X}\sum{Y'} \over n \sum{X^2}-(\sum{X})^2}
$$
$$
a = \bar{Y}'-b\bar{X}
$$
# Potential
$$
Y = aX^b
$$
$$
log{Y} = log{a} + b log{X}
$$
$$
Y' = a' + bX'
$$
$$
b= {n \sum{X'Y'}-\sum{X'}\sum{Y'} \over n \sum{X'^2}-(\sum{X'})^2}
$$
$$
a' = \bar{Y}'-b\bar{X}'
$$

# Creciente

$$
Y = {aX \over X+b}
$$
$$
1/Y = {X+b \over aX}
$$
$$
Y' = {{1\over a} + {{b\over a}X'}}
$$
