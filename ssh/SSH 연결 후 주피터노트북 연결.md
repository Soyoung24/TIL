## SSH 연결 후 주피터노트북 연결

git bash에서 ssh로 서버에 접속한 후에 로컬 chrome 창에 jupyter notebook을 연결해서 쓰고 싶었다. 

석사때 연구실에서 설정한 적이 있는데 그때 정리했던 자료를 찾아가면서 연결했다.

주피터 노트북 연결하는 부분만 정리하였다.  (주피터 노트북이 이미 설치 되어있는 환경에서 시작)

[참고한 블로그](https://velog.io/@jaeha0725/jupyter-notebook-%EC%84%9C%EB%B2%84-%EC%97%B0%EA%B2%B0-SSH-%EC%97%B0%EA%B2%B0)



#### ssh 연결

------

```
$ ssh 계정이름@ip주소 -p 포트번호
```



#### jupyter notebook config 파일 만들기

---

```
$ jupyter notebook --generate-config
```



#### 비밀번호 설정하기

---

```
$ python
$ from notebook.auth import passwd
$ passwd()

#나오는 결과 복사하기 (마우스 사용 또는 alt w)
```



#### 생성된 파일 들어간다.

---

경로: /.jupyter/jupyter_notebook_config.py

```
<아래 내용으로 수정(c앞에 # 유의)>

설정할 항목들:
## 패스워드 만드는것은 웹 참고
c.NotebookApp.password ='아까 복사한 비밀번호 붙여넣기'

#실행과 동시에 web-browser를 실행하지 않게 한다.
c.NotebookApp.open_browser = False
#시작 디렉터리를 변경한다.
#c.NotebookApp.notebook_dir = ''

# The IP address the notebook server will listen on.

c.NotebookApp.ip = 'ip 주소'
c.NotebookApp.port_retries = 5
c.NotebookApp.port = 포트번호 맘대로 설정해도 될듯
```



#### 저장한 후에 git bash에 `jupyter notebook` 이라고 치면 url이 뜬다.

chrome 주소창에 `ip주소:포트번호` 치면 jupyter notebook으로 연결된다!