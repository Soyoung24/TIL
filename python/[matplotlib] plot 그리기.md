## [matplotlib] plot 그리기

plot을 그릴 때 list로 subplot 위치를 만든 다음 그리면 좋다.

 

#### subplot 활용하기

---

```python
import matplotlib.pyplot as plt

fig = fig = plt.figure() if 'fig' not in locals() else fig

fig.clf() # figure 초기화

ax_list = [fig.add_subplot(231),
           fig.add_subplot(232),
           fig.add_subplot(233),
           fig.add_subplot(212)]
```



