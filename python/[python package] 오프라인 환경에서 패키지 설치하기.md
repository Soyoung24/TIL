# [python package] 오프라인 환경에서 패키지 설치하기

오프라인 환경에서 python을 이용해야할 때가 있다. 그때 활용하면 좋을 방법!

이 [블로그](https://sguys99.github.io/it05)에 쉽게 잘 설명되어 있다. 



## 1. 파이썬 패키지 설치파일 다운로드 받기 

먼저 인터넷이 되는 환경에서 파이썬 패키지 설치파일을 다운로드 받아야한다.



- 패키지를 저장할 폴더 생성 (폴더를 zip해서 오프라인 pc로 옮길 것이다)

  ```bash
  (base) C:\>mkdir pkg
  (base) C:\>cd pkg
  (base) C:\pkg>
  ```

  

- `pip download 패키지명==버전번호` 하면 패키지 설치파일이 다운로드 받아진다.

  ```bash
  (base) C:\pkg> pip download numpy==1.19.5
  ```

  

- 패키지를 다운로드 하면서 같은 폴더 안에 requirements.txt 파일을 생성하여 저장한 패키지명과 정보를 적는다.

  ```
  numpy==1.19.5
  pandas==1.2.7
  ```

  (pip freeze를 해서 버전을 확인할 수도 있다.)



## 2. 오프라인 pc에 패키지 설치하기

위에서 패키지 설치파일과 requirements.txt가 들어있는 폴더를 압축하여 오프라인 pc로 옮긴다.

그리고 특정 폴더에 unzip 해준다.

unzip된 폴더로 위치를 옮긴다. (ex `cd pkg`)



- 오프라인 패키지를 설치하는 명령

  ```bash
  (base) C:\pkg> pip install --no-index --find-links="./" -r requirements.txt
  ```

  