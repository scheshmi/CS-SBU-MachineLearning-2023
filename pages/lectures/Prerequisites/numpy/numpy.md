---
layout: default
title: Numpy
parent: Prerequisites
grand_parent: Lectures
nav_order: 1
has_children: false
permalink: /lectures/Prerequisites/numpy/numpy
---




NumPy, short for Numerical Python, is the fundamental package required for hig performance scientific computing and data analysis.Here are some of the things it provides:
- ndarray, a fast and space-efficient multidimensional array providing vectorized arithmetic operations and sophisticated broadcasting capabilities
- Standard mathematical functions for fast operations on entire arrays of data without having to write loops
- Linear algebra, random number generation, and Fourier transform capabilities
- Tools for integrating code written in C, C++, and Fortran

The main areas of functionality of this package are:
- Fast vectorized array operations for data munging and cleaning, subsetting and filtering, transformation, and any other kinds of computations
- Common array algorithms like sorting, unique, and set operations
- Efficient descriptive statistics and aggregating/summarizing data
- Data alignment and relational data manipulations for merging and joining together heterogeneous data sets
- Expressing conditional logic as array expressions instead of loops with if-elifelse branches
- Group-wise data manipulations (aggregation, transformation, function application).


```python
import numpy as np
```

### Creating Arrays
Create a list and convert it to a numpy array



```python
mylist = [1, 2, 3]
x = np.array(mylist)
x
```




    array([1, 2, 3])



Or just pass in a list directly


```python
y = np.array([4, 5, 6])
y
```




    array([4, 5, 6])




```python
type(y) 
```




    numpy.ndarray



Pass in a list of lists to create a multidimensional array.


```python
m = np.array([[7, 8, 9], [10, 11, 12]])
m
```




    array([[ 7,  8,  9],
           [10, 11, 12]])



Use the shape method to find the dimensions of the array. (rows, columns)


```python
np.shape(m)
```




    (2, 3)



 in ndarrays, all elements must have same datatype; numpy transforms automatically


```python
l = [1, 2.5, "Dog", True] #lists can store different datatypes

for i in l:
    print(type(i))

a = np.array(l) 
print(a)

for i in a:
    print(type(i))
```

    <class 'int'>
    <class 'float'>
    <class 'str'>
    <class 'bool'>
    ['1' '2.5' 'Dog' 'True']
    <class 'numpy.str_'>
    <class 'numpy.str_'>
    <class 'numpy.str_'>
    <class 'numpy.str_'>
    

arange returns evenly spaced values within a given interval.


```python
n = np.arange(0, 30, 2) # start at 0 count up by 2, stop before 30
n
```




    array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28])



reshape returns an array with the same data with a new shape.


```python
n = n.reshape(3, 5) # reshape array to be 3x5
n
```




    array([[ 0,  2,  4,  6,  8],
           [10, 12, 14, 16, 18],
           [20, 22, 24, 26, 28]])



linspace returns evenly spaced numbers over a specified interval.


```python
o = np.linspace(0, 4, 9) # return 9 evenly spaced values from 0 to 4
o
```




    array([0. , 0.5, 1. , 1.5, 2. , 2.5, 3. , 3.5, 4. ])



resize changes the shape and size of array in-place.


```python
o.resize(3, 3)
o
```




    array([[0. , 0.5, 1. ],
           [1.5, 2. , 2.5],
           [3. , 3.5, 4. ]])



ones returns a new array of given shape and type, filled with ones.


```python
np.ones((3, 2))
```




    array([[1., 1.],
           [1., 1.],
           [1., 1.]])



zeros returns a new array of given shape and type, filled with zeros.


```python
np.zeros((2, 3))
```




    array([[0., 0., 0.],
           [0., 0., 0.]])



eye returns a 2-D array with ones on the diagonal and zeros elsewhere.


```python
np.eye(3)
```




    array([[1., 0., 0.],
           [0., 1., 0.],
           [0., 0., 1.]])



diag extracts a diagonal or constructs a diagonal array.


```python
print(y)
np.diag(y)
```

    [4 5 6]
    




    array([[4, 0, 0],
           [0, 5, 0],
           [0, 0, 6]])




```python
print(o)
np.diag(o)
```

    [[0.  0.5 1. ]
     [1.5 2.  2.5]
     [3.  3.5 4. ]]
    




    array([0., 2., 4.])



Create an array using repeating list (or use np.tile)


```python
np.array([1, 2, 3] * 3)
```




    array([1, 2, 3, 1, 2, 3, 1, 2, 3])




```python
a = np.array([1, 2, 3])
np.tile(a, 3)
```




    array([1, 2, 3, 1, 2, 3, 1, 2, 3])



Repeat elements of an array using repeat.


```python
np.repeat([1, 2, 3], 3)
```




    array([1, 1, 1, 2, 2, 2, 3, 3, 3])



### Combining Arrays


```python
p = np.ones([2, 3], int)
p
```




    array([[1, 1, 1],
           [1, 1, 1]])



Use vstack to stack arrays in sequence vertically (row wise).


```python
np.vstack([p, 2*p])
```




    array([[1, 1, 1],
           [1, 1, 1],
           [2, 2, 2],
           [2, 2, 2]])



Use hstack to stack arrays in sequence horizontally (column wise).


```python
np.hstack([p, 2*p])
```




    array([[1, 1, 1, 2, 2, 2],
           [1, 1, 1, 2, 2, 2]])



### Operations

Use +, -, *, / and ** to perform element wise addition, subtraction, multiplication, division and power.


```python
print(x + y) # elementwise addition     [1 2 3] + [4 5 6] = [5  7  9]
print(x - y) # elementwise subtraction  [1 2 3] - [4 5 6] = [-3 -3 -3]
```

    [5 7 9]
    [-3 -3 -3]
    


```python
print(x * y) # elementwise multiplication  [1 2 3] * [4 5 6] = [4  10  18]
print(x / y) # elementwise divison         [1 2 3] / [4 5 6] = [0.25  0.4  0.5]
```

    [ 4 10 18]
    [0.25 0.4  0.5 ]
    


```python
print(x**2) # elementwise power  [1 2 3] ^2 =  [1 4 9]
```

    [1 4 9]
    


```python
np.sqrt(x)
```




    array([1.        , 1.41421356, 1.73205081])




```python
np.exp(x)
```




    array([ 2.71828183,  7.3890561 , 20.08553692])




```python
np.log(x)
```




    array([0.        , 0.69314718, 1.09861229])




```python
np.ceil(np.log(x))
```




    array([0., 1., 2.])




```python
np.floor(np.log(x))
```




    array([0., 0., 1.])




```python
np.abs(x)
```




    array([1, 2, 3])




```python
np.around([-3.23, -0.76, 1.44, 2.65, ], decimals = 0) #evenly round all elements to the given number of decimals.
```




    array([-3., -1.,  1.,  3.])



#### Dot Product


```python
print(x, y)
x.dot(y) # dot product  1*4 + 2*5 + 3*6
```

    [1 2 3] [4 5 6]
    




    32




```python
z = np.array([y, y**2])
print(z)
print(np.shape(z))
print(len(z)) # number of rows of array
```

    [[ 4  5  6]
     [16 25 36]]
    (2, 3)
    2
    

Let's look at transposing arrays. Transposing permutes the dimensions of the array.


```python
z.T
```




    array([[ 4, 16],
           [ 5, 25],
           [ 6, 36]])




```python
z.T.shape
```




    (3, 2)



Use .dtype to see the data type of the elements in the array.


```python
z.dtype
```




    dtype('int32')



Use .astype to cast to a specific type.


```python
z = z.astype('f')
z.dtype
```




    dtype('float32')



### Math Functions


```python
a = np.array([-4, -2, 1, 3, 5])
```


```python
a.sum()
```




    3




```python
a.max()
```




    5




```python
a.min()
```




    -4




```python
a.mean()
```




    0.6




```python
a.std()
```




    3.2619012860600183




```python
a.var()
```




    10.64




```python
np.percentile(a, 3)
```




    -3.76



##### Covariance
Covariance is an indicator of the extent to which 2 random variables are dependent on each other. A higher number denotes higher dependency. changes in scale affects covariance.


```python
aa = np.random.random((3, 3))
aa
```




    array([[0.38109917, 0.50598335, 0.31684724],
           [0.19499768, 0.46588364, 0.10965197],
           [0.82519221, 0.92736672, 0.90446043]])




```python
np.cov(aa) #covariance matrix
```




    array([[0.00924947, 0.01778154, 0.00199988],
           [0.01778154, 0.03459402, 0.0048454 ],
           [0.00199988, 0.0048454 , 0.00287463]])



##### Correlation
Correlation is a statistical measure that indicates how strongly two variables are related. changes in scale does not affect correlation.


```python
np.corrcoef(aa) #correlation matrix
```




    array([[1.        , 0.99405522, 0.38784076],
           [0.99405522, 1.        , 0.48589001],
           [0.38784076, 0.48589001, 1.        ]])



argmax and argmin return the index of the maximum and minimum values in the array.


```python
a.argmax()
```




    4




```python
a.argmin()
```




    0



### Indexing / Slicing


```python
s = np.arange(0, 13, 1) ** 2
s
```




    array([  0,   1,   4,   9,  16,  25,  36,  49,  64,  81, 100, 121, 144],
          dtype=int32)



Use bracket notation to get the value at a specific index. Remember that indexing starts at 0.


```python
s[0], s[4], s[-1]
```




    (0, 16, 144)



Use : to indicate a range. array[start:stop]

Leaving start or stop empty will default to the beginning/end of the array.


```python
s[1:5]
```




    array([ 1,  4,  9, 16], dtype=int32)



Use negatives to count from the back.


```python
s[-4:]
```




    array([ 81, 100, 121, 144], dtype=int32)



A second : can be used to indicate step-size. array[start:stop:stepsize]

Here we are starting 5th element from the end, and counting backwards by 3 until the beginning of the array is reached.


```python
s[-5::-3]
```




    array([64, 25,  4], dtype=int32)



Let's look at a multidimensional array.


```python
r = np.arange(36)
r.resize((6, 6))
r
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 31, 32, 33, 34, 35]])



Use bracket notation to slice: array[row, column]


```python
r[2, 2]
```




    14



And use : to select a range of rows or columns


```python
r[3, 3:7]
```




    array([21, 22, 23])



Here we are selecting all the rows up to (and not including) row 2, and all the columns up to (and not including) the last column.


```python
r[:2, :-1]
```




    array([[ 0,  1,  2,  3,  4],
           [ 6,  7,  8,  9, 10]])



This is a slice of the last row, and only every other element.


```python
r[-1, 0:-1:2]
```




    array([30, 32, 34])



We can also perform conditional indexing. Here we are selecting values from the array that are greater than 30. (Also see np.where)


```python
r[r > 30]
```




    array([31, 32, 33, 34, 35])



Here we are assigning all values in the array that are greater than 30 to the value of 30.


```python
r[r > 30] = 30
r
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11],
           [12, 13, 14, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 30, 30, 30, 30, 30]])




```python
mask1 = (r > 5) & (r < 8) #element-wise check if greater 5 and smaller 8 (logical and) 
mask2 = (r > 5) | (r < 8) #element-wise check if greater 5 or smaller 8 (logical or)
mask3 = ~((r > 5) & (r < 8)) #the opposite of mask1
```


```python
r[mask1]
```




    array([6, 7])




```python
r[mask2]
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 30, 30, 30,
           30, 30])




```python
r[mask3]
```




    array([ 0,  1,  2,  3,  4,  5,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17, 18,
           19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 30, 30, 30, 30, 30])



### Copying Data
Be careful with copying and modifying arrays in NumPy!

r2 is a slice of r


```python
r2 = r[:3,:3]
r2
```




    array([[ 0,  1,  2],
           [ 6,  7,  8],
           [12, 13, 14]])



Set this slice's values to zero ([:] selects the entire array)


```python
r2[:] = 0
r2
```




    array([[0, 0, 0],
           [0, 0, 0],
           [0, 0, 0]])



r has also been changed!


```python
r
```




    array([[ 0,  0,  0,  3,  4,  5],
           [ 0,  0,  0,  9, 10, 11],
           [ 0,  0,  0, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 30, 30, 30, 30, 30]])



To avoid this, use r.copy to create a copy that will not affect the original array


```python
r_copy = r.copy()
r_copy
```




    array([[ 0,  0,  0,  3,  4,  5],
           [ 0,  0,  0,  9, 10, 11],
           [ 0,  0,  0, 15, 16, 17],
           [18, 19, 20, 21, 22, 23],
           [24, 25, 26, 27, 28, 29],
           [30, 30, 30, 30, 30, 30]])



Now when r_copy is modified, r will not be changed.


```python
r_copy[:] = 10
print(r_copy, '\n')
print(r)
```

    [[10 10 10 10 10 10]
     [10 10 10 10 10 10]
     [10 10 10 10 10 10]
     [10 10 10 10 10 10]
     [10 10 10 10 10 10]
     [10 10 10 10 10 10]] 
    
    [[ 0  0  0  3  4  5]
     [ 0  0  0  9 10 11]
     [ 0  0  0 15 16 17]
     [18 19 20 21 22 23]
     [24 25 26 27 28 29]
     [30 30 30 30 30 30]]
    

### Iterating Over Arrays
Let's create a new 4 by 3 array of random numbers 0-9.



```python
test = np.random.randint(0,10,(4,3))
test
```




    array([[2, 9, 7],
           [6, 9, 0],
           [8, 4, 0],
           [5, 3, 4]])



Iterate by row:


```python
for row in test:
    print(row)
```

    [2 9 7]
    [6 9 0]
    [8 4 0]
    [5 3 4]
    

Iterate by index:


```python
for i in range(len(test)):
    print(test[i])
```

    [2 9 7]
    [6 9 0]
    [8 4 0]
    [5 3 4]
    

Iterate by row and index:


```python
for i, row in enumerate(test):
    print('row', i, 'is', row)
```

    row 0 is [2 9 7]
    row 1 is [6 9 0]
    row 2 is [8 4 0]
    row 3 is [5 3 4]
    

Use zip to iterate over multiple iterables.


```python
test2 = test**2
test2
```




    array([[ 4, 81, 49],
           [36, 81,  0],
           [64, 16,  0],
           [25,  9, 16]], dtype=int32)




```python
for i, j in zip(test, test2):
    print(i,'+',j,'=',i+j)
```

    [2 9 7] + [ 4 81 49] = [ 6 90 56]
    [6 9 0] + [36 81  0] = [42 90  0]
    [8 4 0] + [64 16  0] = [72 20  0]
    [5 3 4] + [25  9 16] = [30 12 20]
    

### Random Numbers


```python
a = np.random.randint(1,101,10) #creating 10 random integers between 1 (incl.) and 101 (excl.)
a
```




    array([57, 33,  4, 14, 69, 92, 33, 27, 51, 85])




```python
np.random.seed(123) #setting a seed enables reproducibility
a = np.random.randint(1,101,10)
a
```




    array([67, 93, 99, 18, 84, 58, 87, 98, 97, 48])




```python
np.random.normal(5, 2,10) #creating 10 normal disctributed numbers with mean 5 and std 2
```




    array([1.76139987, 2.77207117, 4.10511856, 8.33680322, 4.71325505,
           3.7616182 , 3.46113306, 6.15349204, 5.25305184, 2.39702205])




```python
b = np.arange(1,101) #creating array b from 1 to 100
b
```




    array([  1,   2,   3,   4,   5,   6,   7,   8,   9,  10,  11,  12,  13,
            14,  15,  16,  17,  18,  19,  20,  21,  22,  23,  24,  25,  26,
            27,  28,  29,  30,  31,  32,  33,  34,  35,  36,  37,  38,  39,
            40,  41,  42,  43,  44,  45,  46,  47,  48,  49,  50,  51,  52,
            53,  54,  55,  56,  57,  58,  59,  60,  61,  62,  63,  64,  65,
            66,  67,  68,  69,  70,  71,  72,  73,  74,  75,  76,  77,  78,
            79,  80,  81,  82,  83,  84,  85,  86,  87,  88,  89,  90,  91,
            92,  93,  94,  95,  96,  97,  98,  99, 100])




```python
np.random.shuffle(b) #randomly shuffle ndarray b
b
```




    array([  5,   3,  96,  64,  73,  34,  37,  25,  67,  89,  17,  39,  30,
             9,   6,   1,  14,  80,  98,  87,  63,  38,  82,  33,  58,  29,
            66,  60,  32,  68,  20,  36,  74,  24,  10,  72, 100,  43,  46,
            47,  84,  75,  40,  95,  22,  12,  99,  88,  81,  61,  90,  97,
            42,  54,  45,  52,  69,  18,  79,  13,  50,  57,  21,  51,  26,
            56,  83,  44,   2,  55,  15,   7,  27,  71,  94,  31,  92,  16,
            19,  78,  23,  11,  59,  91,  76,  65,  70,   4,  41,  77,  35,
            28,  86,  53,  93,   8,  49,  62,  48,  85])




```python
b.sort() #sorting ndarray b again
b[::-1] #sorting in reverse order
```




    array([100,  99,  98,  97,  96,  95,  94,  93,  92,  91,  90,  89,  88,
            87,  86,  85,  84,  83,  82,  81,  80,  79,  78,  77,  76,  75,
            74,  73,  72,  71,  70,  69,  68,  67,  66,  65,  64,  63,  62,
            61,  60,  59,  58,  57,  56,  55,  54,  53,  52,  51,  50,  49,
            48,  47,  46,  45,  44,  43,  42,  41,  40,  39,  38,  37,  36,
            35,  34,  33,  32,  31,  30,  29,  28,  27,  26,  25,  24,  23,
            22,  21,  20,  19,  18,  17,  16,  15,  14,  13,  12,  11,  10,
             9,   8,   7,   6,   5,   4,   3,   2,   1])




```python
np.random.seed(123)
b1 = np.random.choice(b, 100, replace = True) #randomly creating a 100 elements sample of ndarray b with/without replacement  
b1
```




    array([ 67,  93,  99,  18,  84,  58,  87,  98,  97,  48,  74,  33,  47,
            97,  26,  84,  79,  37,  97,  81,  69,  50,  56,  68,   3,  85,
            40,  67,  85,  48,  62,  49,   8, 100,  93,  53,  98,  86,  95,
            28,  35,  98,  77,  41,   4,  70,  65,  76,  35,  59,  11,  23,
            78,  19,  16,  28,  31,  53,  71,  27,  81,   7,  15,  76,  55,
            72,   2,  44,  59,  56,  26,  51,  85,  57,  50,  13,  19,  82,
             2,  52,  45,  49,  57,  92,  50,  87,   4,  68,  12,  22,  90,
            99,   4,  12,   4,  95,   7,  10,  88,  15])




```python
b1.sort() #sorting b1
b1
```




    array([  2,   2,   3,   4,   4,   4,   4,   7,   7,   8,  10,  11,  12,
            12,  13,  15,  15,  16,  18,  19,  19,  22,  23,  26,  26,  27,
            28,  28,  31,  33,  35,  35,  37,  40,  41,  44,  45,  47,  48,
            48,  49,  49,  50,  50,  50,  51,  52,  53,  53,  55,  56,  56,
            57,  57,  58,  59,  59,  62,  65,  67,  67,  68,  68,  69,  70,
            71,  72,  74,  76,  76,  77,  78,  79,  81,  81,  82,  84,  84,
            85,  85,  85,  86,  87,  87,  88,  90,  92,  93,  93,  95,  95,
            97,  97,  97,  98,  98,  98,  99,  99, 100])




```python
np.unique(b1) #unique elements of b1
```




    array([  2,   3,   4,   7,   8,  10,  11,  12,  13,  15,  16,  18,  19,
            22,  23,  26,  27,  28,  31,  33,  35,  37,  40,  41,  44,  45,
            47,  48,  49,  50,  51,  52,  53,  55,  56,  57,  58,  59,  62,
            65,  67,  68,  69,  70,  71,  72,  74,  76,  77,  78,  79,  81,
            82,  84,  85,  86,  87,  88,  90,  92,  93,  95,  97,  98,  99,
           100])




```python
np.array(list(set(b1))) #same
```




    array([  2,   3,   4,   7,   8,  10,  11,  12,  13,  15,  16,  18,  19,
            22,  23,  26,  27,  28,  31,  33,  35,  37,  40,  41,  44,  45,
            47,  48,  49,  50,  51,  52,  53,  55,  56,  57,  58,  59,  62,
            65,  67,  68,  69,  70,  71,  72,  74,  76,  77,  78,  79,  81,
            82,  84,  85,  86,  87,  88,  90,  92,  93,  95,  97,  98,  99,
           100])




```python
np.unique(b1).size #how many unique elements?
```




    66




```python
np.unique(b1, return_index= True, return_counts=True) #.unique()-method is quite informative
```




    (array([  2,   3,   4,   7,   8,  10,  11,  12,  13,  15,  16,  18,  19,
             22,  23,  26,  27,  28,  31,  33,  35,  37,  40,  41,  44,  45,
             47,  48,  49,  50,  51,  52,  53,  55,  56,  57,  58,  59,  62,
             65,  67,  68,  69,  70,  71,  72,  74,  76,  77,  78,  79,  81,
             82,  84,  85,  86,  87,  88,  90,  92,  93,  95,  97,  98,  99,
            100]),
     array([ 0,  2,  3,  7,  9, 10, 11, 12, 14, 15, 17, 18, 19, 21, 22, 23, 25,
            26, 28, 29, 30, 32, 33, 34, 35, 36, 37, 38, 40, 42, 45, 46, 47, 49,
            50, 52, 54, 55, 57, 58, 59, 61, 63, 64, 65, 66, 67, 68, 70, 71, 72,
            73, 75, 76, 78, 81, 82, 84, 85, 86, 87, 89, 91, 94, 97, 99],
           dtype=int64),
     array([2, 1, 4, 2, 1, 1, 1, 2, 1, 2, 1, 1, 2, 1, 1, 2, 1, 2, 1, 1, 2, 1,
            1, 1, 1, 1, 1, 2, 2, 3, 1, 1, 2, 1, 2, 2, 1, 2, 1, 1, 2, 2, 1, 1,
            1, 1, 1, 2, 1, 1, 1, 2, 1, 2, 3, 1, 2, 1, 1, 1, 2, 2, 3, 3, 2, 1],
           dtype=int64))



### Performance


```python
size = 1000000 #number of elements
a = np.arange(size) #ndarray 
l = list(range(size)) #list
```


```python
%timeit a+2 #ndarray: measuring time for element-wise addition
```

    1.47 ms ± 60.4 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python
%timeit [i+2 for i in l] #list: measuring time for element-wise addition
```

    64.7 ms ± 1.8 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
    


```python
%timeit a*2 #multiplication
```

    1.68 ms ± 63.9 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python
%timeit [i*2 for i in l] #multiplication
```

    66.9 ms ± 2.34 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
    


```python
%timeit a**2 #square
```

    1.67 ms ± 76.1 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python
%timeit [i**2 for i in l] #square
```

    251 ms ± 4.37 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    


```python
%timeit np.sqrt(a) #square root
```

    3.37 ms ± 187 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
    


```python
%timeit [i**0.5 for i in l] #square root
```

    198 ms ± 1.11 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    

Case Study Numpy vs. Python Standard Library


```python
%timeit (np.random.randint(1,11,100*10000).reshape(10000,100) == 1).sum(axis = 1).mean()
```

    16.1 ms ± 220 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
    


```python
import random

def simulation(): # using nested loops, if statements and lists
    results = []
    for _ in range(10000):    
        l = []
        for _ in range(100):
            if random.randint(1,10) == 1:
                l.append(True)
            else:
                l.append(False)
        results.append(sum(l))
    return (sum(results) / len(results))
```


```python
%timeit simulation()
```

    757 ms ± 12 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    

### References
- Applied data science with python by Michigan university, Coursera
- Python for data analysis book by O'Reilly
- Pandas Bootcamp by Udemy
