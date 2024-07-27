---
title: Ci Items
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
def value_list(t_2d):
    return([[cell.value for cell in row] for row in t_2d])
```

```{.python.marimo}
wb = openpyxl.load_workbook('kin-ts.xlsx')

print(type(wb))
print(wb.sheetnames)
```

```{.python.marimo}
sheet = wb['支出金額（月）']
```

```{.python.marimo}
month = value_list(sheet['Q12:KW12'])[0]
month = [''.join(ii.split()) for ii in month]

xt = np.arange('2000-01-01', '2024-06-01', dtype='datetime64[M]')
print(xt.shape)

print(len(month), len(xt))
print(month[:12])
print(xt[:12])
```

```{.python.marimo}
ll = sheet['H70:N190']
label = [[cell.value for cell in row  if cell.value != None] for row in ll]

print(len(label), len(label[0]))
print(label[:5][:])
```

```{.python.marimo}
data = value_list(sheet['Q70:KW190'])
data = np.array(data, dtype = 'i8')

print(data.shape)
```

```{.python.marimo}
np.savez('items', month = xt, label = label, data = data)
```