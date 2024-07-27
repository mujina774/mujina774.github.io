---
title: Consumerindex
marimo-version: 0.7.8
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
def value_list(t_2d):
    return([[cell.value for cell in row] for row in t_2d])
```

```{.python.marimo}
wb = openpyxl.load_workbook('season-k.xlsx')

print(type(wb))
print(wb.sheetnames)
```

```{.python.marimo}
sheet = wb['指数']

print(type(sheet))
```

```{.python.marimo}
label = value_list(sheet['G7:M7'])

print(label)
```

```{.python.marimo}
data = value_list(sheet['G13:M305'])
data = np.array(data, dtype = 'f8')

print(data.shape)
```

```{.python.marimo}
xt = np.arange('2000-01-01', '2024-06-01', dtype='datetime64[M]')

print(xt[290:])
```

```{.python.marimo}
np.savez('mainIndex', month = xt, data = data, label = label)
```