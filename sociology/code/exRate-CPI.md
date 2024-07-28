---
title: Exrate Cpi
marimo-version: 0.7.12
width: medium
---

```{.python.marimo}
import matplotlib.pyplot as plt
import numpy as np
import matplotlib

matplotlib.rc('font', family='BIZ UDGothic')
```

```{.python.marimo}
data = np.load('npCPI.npz', allow_pickle = True)
print(data.files)
```

```{.python.marimo}
index = data['index']
x = data['months']
cpi = data['data']
```

```{.python.marimo}
print(index, '\n', len(index))
print(cpi.shape)
```

```{.python.marimo}
print(x[120:124])
```

```{.python.marimo}
xt = x[120:]
cpi0 = cpi[120:, :]
```

```{.python.marimo}
import marimo as mo
```

為替レート

```{.python.marimo}
ee = np.load('eexchangeRate.npz', allow_pickle = True)
print(ee.files)
```

```{.python.marimo}
idxEe = ee['label'][1]
xe = ee['month']
eex = ee['data'][:, 1]
print(idxEe, '\t', eex.shape, '\t', len(xe))
```

```{.python.marimo}
ex = np.load('exchangeRate.npz', allow_pickle = True)
print(ex.files)
```

```{.python.marimo}
idxEx = ex['label']
xex = ex['month']
exx = ex['data']
print(idxEx, '\t', exx.shape, '\t', len(xex))
```

```{.python.marimo}
print(xe[480:492])
```

```{.python.marimo}
norm = np.average(exx[480:492])
exx0 = 100 * norm / exx
```

```{.python.marimo}
fig = plt.figure(figsize = (10, 6)) 
ax = fig.add_subplot(1,1,1)

l = [0, 6, 9]
for i in l:
    ax.scatter(xt, cpi0[:, i], s = 3, marker = '.', label = index[i + 1])
#    ax.plot(xt, cpi0[:, i], linewidth = .8, label = index[i + 1])
ax.set_ylim(0, 160)
ax.set_xlabel("Year")
ax.set_ylabel("消費者物価指数、 2020年平均=100")
ax.legend(loc = 'lower right')

ax1 = ax.twinx() 
ax1.scatter(xex, exx0, c='red', s = 3, marker = '.', label = idxEx) 
ax1 .set_ylabel("円・ドルレート、 2020年平均=100")
ax1.set_ylim(0, 160)
ax1.legend(loc = 'upper left')
 
ax.spines['top'].set_visible(False) 
ax1.spines['top'].set_visible(False) 
# plt.savefig("CPI-EXR.png")   
plt.show()
```