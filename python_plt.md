## 用matplot画图的一些函数

### 1.定义图像窗口  
`plt.figure()`

### 2.显示图像
`plt.show()`

### 3.画线  
`plt.plot(x, y, linewidth = '1', label = "test", color=' coral ', linestyle=':', marker='|')`

* **linestyle可选参数:** 

| linestyle | description        |
| --------- |:------------------:|
| '-'       | solid line style   |
| '--'      | dashed line style  | 
| '-.'      | dash-dot line styl |
| ':'       | dotted line style  |
 
 * **marker可选参数:**
 
| marker | description           |
| -------|:---------------------:|
| '.'    | point marker          |
| ','    | pixel marker          | 
| 'o'    | circle marker         |
| 'v'    | triangle_down marker  |
| '^'    | triangle_up marker    |
| '<'    | triangle_left marker  | 
| '>'    | triangle_right marker |     
|'1'     | tri_down marker       |
|'2'     | tri_up marker         |
|'3'     | tri_left marker       |
|'4'     | tri_right marker      |
|'s'     | square marker         |
|'p'     | pentagon marker       |
|'*'     | star marker           |
|'h'     | hexagon1 marker       |
|'H'     | hexagon2 marker       |
|'+'     | plus marker           |
|'x'     | x marker              |
|'D'     | diamond marker        |
|'d'     | thin_diamond marker   |
|'|'     | vline marker          |
|'_'     | hline marker          |
 
* **colork可选参数：**

![icon](https://github.com/lhzhong/iNote/blob/master/pic/plt_color.png)

### 4.设置坐标范围
```
plt.axis([xmin, xmax, ymin, ymax])
plt.xlim((xmin, xmax)) 
plt.ylim((ymin, ymax))
```

### 5.设置坐标名称
```
plt.xlabel('X')
plt.ylabel('Y')
```

### 6.设置坐标刻度
```
plt.xticks([x1,x2,x3,…])
plt.yticks([y1,y2,y3,..])
```
> 坐标点可以通过np.arange np.linsapce等生成  
如果要不显示坐标刻度：  
`Plt.xticks([])`  
如果坐标刻度要设置成名称形式：  
`plt.yticks([-2, -1.8, -1, 1.22, 3],[r'$really\ bad$', r'$bad$', r'$normal$', r'$good$', r'$really\ good$'])`
