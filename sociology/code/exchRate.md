---
title: Exchrate
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
fn = 'fm08_m_1.csv'
```

```{.python.marimo}
with open(fn, encoding = 'cp932') as f:
    l1 = f.read().splitlines()
    
print(len(l1))
```

```{.python.marimo}
label = l1[3].split(',')[2]
print(label)
```

```{.python.marimo}
print(l1[9])
```

```{.python.marimo}
m = []
ll = []
for i in l1[9:]:
    m.append(i.split(',')[0])
    ll.append(i.split(',')[2])

print(len(m), len(ll))
```

```{.python.marimo}
mon = [datetime.datetime.strptime(mm, "%Y/%m") for mm in m]
```

```{.python.marimo}
data = np.array(ll, dtype = 'f8')
```

```{.python.marimo}
np.savez('exchangeRate', label = label, month = mon, data = data)
```