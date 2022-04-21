## WandB 간단 사용 방법 

MLOps Tool 이라고 한다.

모델 실험 관리를 해줄 수 있는 툴!

Weight and Biases라서 WandB라고 한다.



wandb에서 프로젝트 이름 설정하고 하니까 어떤식으로 하라고 튜토리얼이 있긴 했다.

내가 강화학습 모델 확인할 때 사용했던 것만 아주 간단히 기록!

https://ndb796.tistory.com/699  나중에 다시 확인해봐도 좋을 것 같다.

  

#### 1. Install wandb

---

$ pip install wandb



#### 2. wandb login

---

$ wandb login 'API key'



#### 3. 파이썬 모델 훈련 코드에 추가

---

- import wandb

  ```python
  import wandb
  import json
  import os; os.environ['WANDB_NOTEBOOK_NAME'] = 'jyp'
  ```

- train 코드에 추가하기 

  epoch 끝나기 전에 그 epoch 결과를 wandb config에 기록!

  ```python
  log_dict = dict()
  log_dict['cum_return'] = cum_r
  wandb.log(log_dict)
  ```

- main 함수에 추가

  - wandb에 하이퍼파라미터 config를 기록한다. 만약 argparse를 이용해서 configuration 정보를 설정했다면 ` wandb.config = vars(config)  ` 이런식으로 해주면 dictionary 형태로 바뀐다.

  ```python
  wandb.config = vars(config)
  # wandb 프로젝트 초기화
  wandb.init(project='rl_AE_1d', entity="fc_rl",
                 config=config)
  ```

  