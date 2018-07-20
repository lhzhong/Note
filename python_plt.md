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

### 7.添加图例  
需要事先在plot函数中设置label内容  
```
plt.plot(x, y1, label='linear line')
plt.legend(loc='upper right')
```
如果没有在plot中设置lable内容，或想单独修改label内容，也可以在legend中传入其他参数，但是这需要plot返回变量  
```
l1, = plt.plot(x, y1, label='linear line')    #l1, 要以逗号结尾, 因为plt.plot() 返回的是一个列表.
l2, = plt.plot(x, y2, color='red', linewidth=1.0, linestyle='--', label='square line')
plt.legend(handles=[l1, l2], labels=['up', 'down'],  loc='best'
```
其中'loc'参数有多种，'best'表示自动分配最佳位置，其余的如下：

| loc           |description|
|---------------|:---------:|
|'best'         | 0         |
|'upper right'  | 1         |
|'upper left'   | 2         |
|'lower left'   | 3         |
|'lower right'  | 4         |
|'right'        | 5         |
|'center left'  | 6         |
|'center right' | 7         |
|'lower center' | 8         |
|'upper center' | 9         |
|'center'       | 10        |

### 8.获取当前坐标轴信息

`plt.gca()` 获取当前坐标轴信息`.spines['right']`设置边框（'right''left''top''bottom'）`.set_color('none')`设置边框颜色  
```
# 比如设置边框
ax = plt.gca()
ax.spines['right'].set_color('none')
# 或者
ax.spines['right'].set_visible(False)
```

### 9.添加注释annotate和text
```
plt.annotate(r'$2x+1=%s$' % y0, xy=(x0, y0), xycoords='data', xytext=(+30, -30),
             textcoords='offset points', fontsize=16,
             arrowprops=dict(arrowstyle='->', connectionstyle="arc3,rad=.2"))

```
> 参数xycoords='data' 是说基于数据的值来选位置, xytext=(+30, -30) 和 textcoords='offset points' 对于标注位置的描述 和 xy 偏差值, arrowprops是对图中箭头类型的一些设置.
```
plt.text(-3.7, 3, r'$This\ is\ the\ some\ text. \mu\ \sigma_i\ \alpha_t$',
         fontdict={'size': 16, 'color': 'r'})

```
> 其中-3.7, 3,是选取text的位置, 空格需要用到转字符\ ,fontdict设置文本字体.

### 10.添加颜色条  
`plt.colorbar()`  
设置 cmap 的几种方式：  
```
plt.imshow(image, cmap=plt.get_cmap('gray_r'))
plt.imshow(image, cmap='gray_r')
```
> cmap参数值见[color example code: colormaps](https://matplotlib.org/examples/color/colormaps_reference.html)
