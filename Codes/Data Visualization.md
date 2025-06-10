# A8 - Data Visualization-1

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `seaborn` & `matplotlib`

```shell
pip install matplotlib seaborn
```

---

## Code blocks

1. Import libraries:

```python3
import seaborn as sns
from matplotlib import pyplot as plt
```

2. Load built-in dataset:

```python3
df=sns.load_dataset('titanic')
df.head()
```

3. Dist plot for age:

```python3
plt.figure(figsize=(6,4))
sns.displot(df['age']) # Use sns.distplot(df['age']) for older versions of seaborn library
plt.show()
```

4. Box plot:

```python3
plt.figure(figsize=(5,3))
bp = sns.boxplot(x='class',y='age',palette='pastel',data=df)
plt.show()
df.describe().transpose()
```

5. Violin plot:

```python3
plt.figure(figsize=(5,4))
vp = sns.violinplot(x='class',y='age',palette='rainbow',data=df)
plt.show()
```

6. Hist plot:

```python3
plt.figure(figsize=(5,4))
pq = sns.histplot(x='fare',bins=10,data=df,hue='survived',kde=False)
for i in pq.containers:
  pq.bar_label(i)
plt.show()
```

7. Scatter plot:

```python3
plt.figure(figsize=(5,4))
st=sns.scatterplot(x='age',y='fare',data=df)
plt.show()
```

8. Scatter plot:

```python3
plt.figure(figsize=(5,4))
kl=sns.scatterplot(x='age',y='fare',data=df,hue='survived')
plt.show()
```

---
