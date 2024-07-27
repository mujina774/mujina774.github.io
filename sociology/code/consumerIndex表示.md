---
title: "Consumerindex\u8868\u793A"
marimo-version: 0.7.12
width: medium
---

```{.python.marimo}
import matplotlib.pyplot as plt
import numpy as np
import matplotlib
import openpyxl
import datetime

matplotlib.rc('font', family='BIZ UDGothic')
```

```{.python.marimo}
data = np.load('mainIndex.npz', allow_pickle = True)

print(data.files)
```

```{.python.marimo}
label = data['label'][0]
x = data['month']
ci = data['data']
```

```{.python.marimo}
print(label)
print(ci.shape)
```

消費性向: 可処分所得 (≒ 実収入) に占める消費支出の割合

```{.python.marimo}
fig = plt.figure(figsize = (10, 6)) 
ax = fig.add_subplot(1,1,1)

l = [4, 5, 3]
for i in l:
    ax.plot(x, ci[:, i], linewidth = .8, label = label[i])
ax.set_ylim(0, 160)
ax.set_xlabel("Year")
ax.set_ylabel("指数 (2020年＝100)")
ax.set_title('主要項目の季節調整値 ― 二人以上の世帯のうち勤労者世帯')
ax.legend(loc = 'lower right')
ax.spines['right'].set_visible(False) 
ax.spines['top'].set_visible(False) 
plt.savefig("CI-long.png")   
plt.show()
```

```{.python.marimo}
import marimo as mo
```