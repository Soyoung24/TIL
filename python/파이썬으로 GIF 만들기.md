## 파이썬으로 GIF 만들기

png 파일로 저장된 이미지를 모아서 gif 영상을 만드는 방법이다.

imageio 패키지를 다운받아야 한다.

그리고 파일명이 001, 002, 003, ..., 011, ... 이런식으로 저장되어 있어야 순서대로 영상이 만들어진다.



같이 프로젝트 했던 박사님께서 알려주신 코드이다.

```python
import os, imageio
from PIL import Image

img_path_base = r'이미지가 저장되어 있는 폴더 주소'
ani_path = os.path.join(img_path_base, '파일명.gif')

path = [os.path.join(img_path_base, img_file) for img_file in [x for x in os.listdir(img_path_base) if '.png' in x]]
paths = [Image.open(i) for i in path]

imageio.mimsave(ani_path, paths, fps=12)
```



