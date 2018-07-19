## pythoon数组拼接的方法对比

**1. list的方法append, extend**
```
x = [[1, 2], [3, 4]]
y = [[2, 4], [6, 8]]
x.append(x)            # x = [[1, 2], [3, 4], [[2, 4], [6, 8]]] 
x.extend(x)            # x = [[1, 2], [3, 4], [2, 4], [6, 8]]
```

**2. numpy的方法append, concatenate**

* np.append(arr, values, axis=None):  
要么一个数组和一个数值；要么两个数组，不能三个及以上数组直接append拼接。append函数返回的始终是一个一维数组。

* np.concatenate((a1,a2,...), axis=0):  
能够一次完成多个数组的拼接。axis=1表示对应行的数组进行拼接
```
x = np.array([[1, 2], [3, 4]])
y = np.array([[2, 4], [6, 8]])
z = np.append(a, b)                   # z = array([1, 2, 3, 4, 2, 4, 6, 8])
z2 = np.concatenate((x, y))           # z2 = array([[1, 2], [3, 4], [2, 4], [6, 8]])
z3 = np.concatenate((x, y), axis=1)   # z3 = array([[1, 2, 2, 4], [3, 4, 6, 8]])
```
