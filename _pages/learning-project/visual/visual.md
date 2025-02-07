---
title: 시각화
layout: single
classes: wide
permalink: /learning-project/visual/
---
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

1. histogram 그리기


```python
score = [21, 78, 89, 57, 75, 99, 98, 87, 70, 65, 88, 95, 94, 55, 93, 83, 78, 62, 65, 77, 80]
plt.hist(score)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_3_0.png)
    

- bins 수 설정


```python
plt.hist(score, bins=5)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_5_0.png)
    


- 누적 histogram 그리기


```python
plt.hist(score, cumulative=True)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_7_0.png)
    


- 차트 type 바꾸기


```python
plt.hist(score, histtype='step')
# 'bar', 'barstacked', 'step', 'stepfilled'
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_9_0.png)
    



```python
data1 = np.random.normal(0, 1, 1000)
data2 = np.random.normal(1, 1, 1000)
# mean, std, count

fig, axs = plt.subplots(2, 2, figsize=(10, 5))

axs[0, 0].hist([data1, data2], bins=30, color=['red', 'blue'], histtype='bar')
axs[0, 0].set_title('Bar')

axs[0, 1].hist([data1, data2], bins=30, color=['red', 'blue'], histtype='barstacked')
axs[0, 1].set_title('Barstacked')

axs[1, 0].hist([data1, data2], bins=30, color=['red', 'blue'], histtype='step')
axs[1, 0].set_title('Step')

axs[1, 1].hist([data1, data2], bins=30, color=['red', 'blue'], histtype='stepfilled')
axs[1, 1].set_title('Stepfilled')

fig.subplots_adjust(hspace=0.5)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_10_0.png)
    


2. pie chart


```python
ratio = [0.25, 0.1, 0.3, 0.35]
grade = ['A', 'B', 'C', 'D']
plt.pie(ratio, labels=grade)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_12_0.png)
    


* 비율 추가


```python
plt.pie(ratio, labels=grade, autopct='%.1f%%')
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_14_0.png)
    


* 설정 변경 : rotation, 방향, 색상, 분리


```python
cmap = plt.get_cmap('tab20c')
colors = cmap(np.arange(len(ratio)) % cmap.N)
# colors = ['blue', 'green', 'cyan', 'orange']

explode = (0.2, 0, 0, 0.1)

plt.pie(ratio, labels=grade, autopct='%.1f%%', startangle=90, counterclock=False, colors=colors, explode=explode)
plt.show()
```

    20



    
![png](/_pages/learning-project/visual/visual_files/visual_16_1.png)
    



```python
np.arange(len(ratio))
```




    array([0, 1, 2, 3])




```python
cmap(np.arange(len(ratio)) % cmap.N)
```

    array([[0.19215686, 0.50980392, 0.74117647, 1.        ],
           [0.41960784, 0.68235294, 0.83921569, 1.        ],
           [0.61960784, 0.79215686, 0.88235294, 1.        ],
           [0.77647059, 0.85882353, 0.9372549 , 1.        ]])



3. 박스플롯


```python
fig, ax = plt.subplots()
bp = ax.boxplot(score, whis=1.5, vert=True, patch_artist=True)

# Get the whisker values
whiskers = [whisker.get_ydata()[1] for whisker in bp['whiskers']]
print("Lower whisker value:", whiskers[0])
print("Upper whisker value:", whiskers[1])

plt.show()
```

    Lower whisker value: 55.0
    Upper whisker value: 99.0



    
![png](/_pages/learning-project/visual/visual_files/visual_22_1.png)
    



```python
score
```
    [21,
     78,
     89,
     57,
     75,
     99,
     98,
     87,
     70,
     65,
     88,
     95,
     94,
     55,
     93,
     83,
     78,
     62,
     65,
     77,
     80]




* 가로로 그리기


```python
plt.boxplot(score, vert=False)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_26_0.png)
    


* 색상 변경


```python
bp = plt.boxplot(score, vert=False, patch_artist=True)
for box in bp['boxes']:
    box.set(color='blue', linewidth=2)
    box.set(facecolor = 'yellow')
for cap in bp['caps']:
    cap.set(color='red', linewidth=2)
for whisker in bp['whiskers']:
    whisker.set(color='orange', linewidth=2)
for median in bp['medians']:
    median.set(color='cyan', linewidth=2)
for flier in bp['fliers']:
    flier.set(marker='s', markerfacecolor='r', markersize=10, markeredgecolor='r')

plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_28_0.png)
    


* 2개 이상의 변수 표시


```python
plt.boxplot([data1, data2])
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_30_0.png)
    


4. 막대차트


```python
fruits = ['apple', 'blueberry', 'cherry', 'orange']
counts = [40, 100, 30, 55]
plt.bar(fruits, counts)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_32_0.png)
    


* 색상지정


```python
colors = ['red', 'blue', 'darkred', 'orange']
plt.bar(fruits, counts, color=colors)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_34_0.png)
    


* 변수 2개


```python
counts2 = [20, 80, 20, 60]
colors2 = ['tomato', 'cornflowerblue', 'indianred', 'gold']

ind = np.arange(len(counts))
width = 0.4

plt.bar(ind, counts, width, color=colors)
# plt.bar(x=ind, height=counts, width=width, color=colors)
plt.bar(ind + width, counts2, width, color=colors2)

plt.xticks(ind + width / 2, fruits)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_36_0.png)
    


* 가로 막대차트


```python
plt.barh(ind, counts, width, color=colors)
plt.barh(ind + width, counts2, width, color=colors2)

plt.yticks(ind + width / 2, fruits)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_38_0.png)
    


5. 산점도


```python
# data1, data2 이용
plt.scatter(data1, data2)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_40_0.png)
    


* 색상, 크기 변경


```python
area = 10
colors = np.random.rand(1000)

plt.scatter(data1, data2, s=area, c=colors, alpha=0.5)
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_42_0.png)
    


* 색상, 크기 : 변수와 연동


```python
data3 = np.random.normal(1, 50, 1000)
```


```python
plt.scatter(data1, data2, s=data3, c=data3, alpha=0.6, cmap='hsv')
plt.show()
```

    /usr/local/lib/python3.10/dist-packages/matplotlib/collections.py:963: RuntimeWarning: invalid value encountered in sqrt
      scale = np.sqrt(self._sizes) * dpi / 72.0 * self._factor



    
![png](/_pages/learning-project/visual/visual_files/visual_45_1.png)
    


* seaborn을 이용한 멀티 산점도


```python
import seaborn as sns
iris = sns.load_dataset("iris")
g = sns.PairGrid(iris, hue="species")
g.map_diag(sns.histplot)
g.map_offdiag(sns.scatterplot)
g.add_legend()
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_47_0.png)
    


6. 히트맵


```python
data_con = [[3, 4, 5], [4, 5, 3], [3, 4, 3]]

plt.imshow(data_con)
# plt.imshow(data_con, cmap='autumn')
plt.colorbar()
plt.show()
```


    
![png](/_pages/learning-project/visual/visual_files/visual_49_0.png)
    

