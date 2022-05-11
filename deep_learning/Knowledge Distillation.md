## Knowledge Distillation

미리 잘 학습된 큰 네트워크(Teacher network) 의 지식을 실제로 사용하고자 하는 작은 네트워크(Student network) 에게 전달하는 것 (출처: https://light-tree.tistory.com/196)

여기서 teacher network의 지식은 Soft label을 의미한다.

(soft label은 classification 모델에서 softmax를 통과하고 나온 클래스별 확률값을 말한다. max 시키기 전의 값! )



[유튜브](https://www.youtube.com/watch?v=pgfsxe8sROQ&t=595s)에서 공부한 내용 중 일부를 기록해놓고자 한다. 대략적인 개념만..

<img width="797" alt="Untitled" src="https://user-images.githubusercontent.com/56706291/167868824-1c6e0d6c-4ac8-442f-a100-e88b67f1df4d.png">

1) Teacher 모델을 미리 학습시킨다. (pretrain, 높은 성능을 확보해놓는다.)

2) 동일한 데이터를 사용해서 Student  모델을 학습시킨다.

​	이때, student 모델은 teacher 모델의 soft label과 실제 label 값을 모두 사용한다. ($L_{soft}, L_{task}$ ) 

​	⇒ student 모델은 teacher 모델의 예측분포와 최대한 유사하도록 학습된다.

3) Student 모델의 loss function은 두 로스를 합한 것이다.

