---
title: "Exchrate(\u4F5C\u56F3)"
marimo-version: 0.7.12
width: medium
---

```{.python.marimo}
import matplotlib.pyplot as plt
import numpy as np
import matplotlib
import matplotlib.dates as dates

matplotlib.rc('font', family='BIZ UDGothic')
```

```{.python.marimo}
data = np.load('eexchangeRate.npz', allow_pickle = True)
print(data.files)
```

```{.python.marimo}
idxEe = data['label'][1]
x = data['month']
eexr = data['data'][:, 1]
print(idxEe)
print(eexr.shape)
```

```{.python.marimo}
exdata = np.load('exchangeRate.npz', allow_pickle = True)
print(exdata.files)
```

```{.python.marimo}
idxEx = exdata['label']
xe = exdata['month']
exr = exdata['data']
```

```{.python.marimo}
print(exr.shape)
```

```{.python.marimo}
print(xe[480:492])
```

```{.python.marimo}
norm = np.average(exr[480:492])
exr0 = 100 * norm / exr 
```

```{.python.marimo}
fig = plt.figure(figsize = (10, 6)) 
ax = fig.add_subplot(1,1,1)

ax.plot(x, eexr, linewidth = .8, label = idxEe)
ax.plot(xe, exr0, linewidth = .8, label = idxEx)
ax.set_ylim(0, 280)
ax.set_xlabel("Year")
ax.set_ylabel(idxEe)
ticks = 60
plt.xticks(x[::ticks])
ax.legend(loc = 'upper right')
ax.spines['right'].set_visible(False) 
ax.spines['top'].set_visible(False) 
# plt.savefig("exchRate.png")   
plt.show()
```