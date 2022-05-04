## [pytorch] Transfer Learning

pretrained model 가져와서 사용할 때, layer 이름 지정해서 freeze 하기



#### Frozen

---

Feature extractor에 대하여 역전파 수행하지 않는다.



모델 불러오기

```python
from torchvision import models
model=models.resnet50(pretrained=True)
```



모델 전체를 freeze 하고 싶으면 아래와 같이 하면 되고, 

```python
for param in model.parameters():
	param.requires_grad = False
```



모델의 마지막 단만 아래와 같이 바꿔주면 fc 파라미터만 학습하게 된다. (trainable parameter가 된다.)

```python
num_ftrs = model.fc.in_features
model.fc = nn.Sequential(nn.Linear(num_ftrs, 10))
```



#### Fine-tuning

---

pretrained model을 불러오고나서 마지막 레이어를 우리 task에 맞춰서 바꾸고, Feature extractor에 대하여 역전파 수행한다. 

```python
from torchvision import models
model=models.resnet50(pretrained=True)

num_ftrs = model.fc.in_features
model.fc = nn.Sequential(nn.Linear(num_ftrs, 10))
```



#### 앞부분은 freeze, 뒷단의 일부 레이어를 trainable layer로 바꾸고 학습시키기

---

![transfer learning](https://user-images.githubusercontent.com/56706291/166637873-d172e79e-ebd8-4e71-b359-2465f7fdb244.PNG)

fc와 layer4만 freeze를 풀고 싶을 때!

```python
for name, child in resnet50_pretrained.named_children():
    for param in child.parameters():
        if name == 'fc' or name == 'layer4':
            param.requires_grad = True
        else: 
            param.requires_grad = False
```



#### 보통 Transfer Learning 할 때 학습시키는 방법

---

1. `pretrained=True`로 모델을 가져와서 뒷단만 freeze를 풀고 학습을 시키던지, 전체를 freeze 풀고 학습을 시킨다.

2. `pretrained=False`로 모델을 가져와서 1에서 학습시킨 모델을 불러오고, 전체를 trainable하게 하고, learning rate를 아주 작게 해서 한번 더 학습 시킨다. (예: lr=0.00005)

   ```python
   face_model = models.resnet50(pretrained=False)
   
   num_ftrs = face_model.fc.in_features
   face_model.fc = nn.Sequential(nn.Linear(num_ftrs, 10))
   
   model_path = 'output_classification_resnet50/model_41_55.72_43.19.pt'
   weights = torch.load(model_path)
   
   face_model.load_state_dict(weights)
   ```

   



**참고한 자료**

- [Pytorch Model 일부 Layer만 Freeze 하기](https://soyoung97.github.io/pytorch-model-%EC%9D%BC%EB%B6%80-layer%EB%A7%8C-freeze-%ED%95%98%EA%B8%B0/)

- [PyTorch의 전이 학습(Transfer Learning)에서 Freezing 여부에 따른 성능 차이 및 유의점](https://ndb796.tistory.com/552)

- [6. ResNet50 Transfer learning & fine tuning 적용하기(이미지 수집부터 분류 모델까지)](https://inhovation97.tistory.com/41)

- [Transfer learning & fine tuning의 다양하고 섬세한 기법](https://inhovation97.tistory.com/31)

