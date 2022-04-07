## [argparse] ArgumentParser에서 bool 값 받기

ArgumentParser에서 type을 `bool`로 지정해주었을 때 default 값으로만 설정이 되고 새로 입력하는 값은 인식을 못했다. 

참고: https://eehoeskrap.tistory.com/521



#### 함수 만들기

---

```python
def str2bool(v):
    if isinstance(v, bool):
        return v
    if v.lower() in ('yes', 'true', 't', 'y', '1'):
        return True
    elif v.lower() in ('no', 'false', 'f', 'n', '0'):
        return False
    else:
        raise argparse.ArgumentTypeError('Boolean value expected.')
```



#### 예시

---

```python
import argparse

def define_argparser():
    p = argparse.ArgumentParser()
    
    p.add_argument('--render', type=str2bool, default=True)
    
    config = p.parse_args()
	return config
```

