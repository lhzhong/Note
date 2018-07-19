## pythoon数组拼接的方法对比

1. list的方法append, extend
```
x = [[1, 2], [3, 4]]
y = [[2, 4], [6, 8]]
x.append(x)  # x = [[1, 2], [3, 4], [[2, 4], [6, 8]]] 
x.extend(x)  # x = [[1, 2], [3, 4], [2, 4], [6, 8]]
```

2. numpy的方法append, concatenate
