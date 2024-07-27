---
title: "Ci Items\u8868\u793A"
marimo-version: 0.7.12
width: medium
---

```{.python.marimo}
import matplotlib.pyplot as plt
import numpy as np
import matplotlib
import datetime

matplotlib.rc('font', family='BIZ UDGothic')
```

```{.python.marimo}
data = np.load('items.npz', allow_pickle = True)

print(data.files)
```

```{.python.marimo}
label = data['label']
x = data['month']
citm = data['data']
```

```{.python.marimo}
print(citm.shape)

for i in range(len(label)):
    print(i, '\t', label[i])
```

```{.python.marimo}
fig = plt.figure(figsize = (10, 6)) 
ax = fig.add_subplot(1,1,1)

l = [0, 41, 46, 61, 79, 84]
for ii in l:
    ax.plot(x, citm[ii, :], linewidth = .8, label = label[ii][1])
ax.set_ylim(0, )
ax.set_xlabel("Year")
ax.set_ylabel("支出")
ax.legend(loc = 'center right', bbox_to_anchor=(1.2, 0.5,))
ax.set_title("支出の内訳 (一部)")
ax.spines['right'].set_visible(False) 
ax.spines['top'].set_visible(False) 
plt.savefig('ci-items.png', bbox_inches='tight') 
plt.show()
```

```{.python.marimo}

```