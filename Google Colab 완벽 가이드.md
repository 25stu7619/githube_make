# Google Colab 완벽 가이드

## 1. Google Colab이란?

Google Colaboratory(줄여서 Colab)는 구글에서 제공하는 무료 클라우드 기반 Jupyter 노트북 환경입니다. 별도의 설치 없이 브라우저에서 Python 코드를 작성하고 실행할 수 있으며, 무료 GPU와 TPU를 제공합니다.

### 주요 특징

- **무료 GPU/TPU 사용**: 머신러닝과 딥러닝 학습에 필요한 하드웨어 무료 제공
- **설치 불필요**: 웹 브라우저만 있으면 즉시 사용 가능
- **Google Drive 연동**: 파일을 쉽게 저장하고 불러올 수 있음
- **협업 기능**: 여러 사람이 동시에 작업 가능
- **주요 라이브러리 사전 설치**: TensorFlow, PyTorch, NumPy 등이 기본 설치됨

## 2. 시작하기

### Colab 접속하기

1. [colab.research.google.com](https://colab.research.google.com) 접속
2. Google 계정으로 로그인
3. **새 노트북** 버튼 클릭

### 새 노트북 만들기

- **파일 > 새 노트북**: 새로운 노트북 생성
- **파일 > 노트북 열기**: 기존 노트북 열기
- **파일 > GitHub에서 노트북 열기**: GitHub 리포지토리의 노트북 불러오기

## 3. 기본 사용법

### 셀(Cell) 사용하기

Colab 노트북은 셀 단위로 구성됩니다. 셀에는 두 가지 유형이 있습니다.

#### 코드 셀
```python
# Python 코드를 작성하고 실행
print("Hello, Colab!")

# 변수 선언
x = 10
y = 20
print(f"합계: {x + y}")
```

**셀 실행 방법:**
- **Shift + Enter**: 셀 실행 후 다음 셀로 이동
- **Ctrl + Enter**: 셀 실행 후 현재 셀에 머물기
- **Alt + Enter**: 셀 실행 후 아래에 새 셀 추가

#### 텍스트 셀

텍스트 셀은 마크다운 형식으로 작성하여 문서화에 사용합니다.

### 셀 추가 및 관리

- **+ 코드**: 코드 셀 추가
- **+ 텍스트**: 텍스트 셀 추가
- 셀 위아래의 화살표로 순서 변경
- 휴지통 아이콘으로 셀 삭제

## 4. 런타임 설정

### 하드웨어 가속기 선택

**런타임 > 런타임 유형 변경**에서 하드웨어를 선택할 수 있습니다.

- **None**: CPU만 사용
- **T4 GPU**: 무료 GPU (일반 사용자)
- **TPU**: Tensor Processing Unit
- **A100 GPU**, **V100 GPU**: Colab Pro/Pro+ 전용

### 런타임 관리

- **런타임 > 모두 실행**: 모든 셀을 순서대로 실행
- **런타임 > 런타임 다시 시작**: 런타임 재시작 (변수 초기화)
- **런타임 > 런타임 다시 시작 및 모두 실행**: 재시작 후 전체 실행
- **런타임 > 런타임 연결 해제 및 삭제**: 현재 세션 종료

⚠️ **주의**: 런타임이 종료되면 변수와 설치한 패키지가 모두 사라집니다.

## 5. 라이브러리 설치 및 임포트

### 사전 설치된 라이브러리 사용

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import tensorflow as tf
import torch
```

### 새 라이브러리 설치

```python
# pip로 설치
!pip install transformers

# 특정 버전 설치
!pip install scikit-learn==1.2.0

# 여러 패키지 동시 설치
!pip install pillow opencv-python requests
```

### apt-get으로 시스템 패키지 설치

```python
# 시스템 레벨 패키지 설치
!apt-get update
!apt-get install -y graphviz
```

## 6. 파일 업로드 및 다운로드

### 파일 업로드

#### 방법 1: 코드로 업로드
```python
from google.colab import files

# 파일 선택 창이 열립니다
uploaded = files.upload()

# 업로드된 파일 확인
for filename in uploaded.keys():
    print(f'업로드된 파일: {filename}')
```

#### 방법 2: 사이드바 사용
왼쪽 사이드바의 폴더 아이콘 클릭 → 업로드 버튼 클릭

### 파일 다운로드

```python
from google.colab import files

# 파일 생성
with open('sample.txt', 'w') as f:
    f.write('Hello, Colab!')

# 파일 다운로드
files.download('sample.txt')
```

## 7. Google Drive 연동

### Drive 마운트

```python
from google.colab import drive

# Google Drive 마운트
drive.mount('/content/drive')

# 마운트 후 경로 예시
# /content/drive/MyDrive/파일명
```

### Drive 파일 읽고 쓰기

```python
# 파일 읽기
with open('/content/drive/MyDrive/data.txt', 'r') as f:
    content = f.read()
    print(content)

# 파일 쓰기
with open('/content/drive/MyDrive/output.txt', 'w') as f:
    f.write('결과 저장')

# pandas로 CSV 읽기
import pandas as pd
df = pd.read_csv('/content/drive/MyDrive/data.csv')
```

## 8. 매직 커맨드

### 유용한 매직 커맨드

```python
# 셀 실행 시간 측정
%%time
import time
time.sleep(2)

# 여러 번 실행하여 평균 시간 측정
%%timeit
sum(range(100))

# 현재 디렉토리 확인
!pwd

# 파일 목록 보기
!ls

# 환경 변수 확인
!echo $PATH

# 현재 작업 디렉토리 변경
%cd /content/drive/MyDrive

# 변수 목록 확인
%who

# 자세한 변수 정보
%whos
```

## 9. GPU 사용하기

### GPU 확인

```python
import tensorflow as tf

# GPU 사용 가능 여부 확인
print("GPU 사용 가능:", tf.config.list_physical_devices('GPU'))

# PyTorch에서 GPU 확인
import torch
print("CUDA 사용 가능:", torch.cuda.is_available())
print("GPU 이름:", torch.cuda.get_device_name(0) if torch.cuda.is_available() else "GPU 없음")
```

### GPU 메모리 확인

```python
# nvidia-smi로 GPU 상태 확인
!nvidia-smi

# PyTorch GPU 메모리 확인
import torch
print(f"할당된 메모리: {torch.cuda.memory_allocated() / 1e9:.2f} GB")
print(f"예약된 메모리: {torch.cuda.memory_reserved() / 1e9:.2f} GB")
```

## 10. 데이터 시각화

### Matplotlib 사용

```python
import matplotlib.pyplot as plt
import numpy as np

# 그래프 그리기
x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y)
plt.title('사인 함수')
plt.xlabel('X')
plt.ylabel('Y')
plt.grid(True)
plt.show()
```

### 인터랙티브 시각화

```python
import plotly.express as px

# Plotly로 인터랙티브 그래프
df = px.data.iris()
fig = px.scatter(df, x='sepal_width', y='sepal_length', color='species')
fig.show()
```

## 11. 유용한 팁

### 단축키

- **Ctrl + M + B**: 아래에 코드 셀 추가
- **Ctrl + M + A**: 위에 코드 셀 추가
- **Ctrl + M + D**: 현재 셀 삭제
- **Ctrl + M + Y**: 셀을 코드 셀로 변환
- **Ctrl + M + M**: 셀을 텍스트 셀로 변환
- **Ctrl + M + H**: 단축키 목록 보기
- **Ctrl + S**: 노트북 저장

### 진행 상황 표시

```python
from tqdm import tqdm
import time

# 진행률 바 표시
for i in tqdm(range(100)):
    time.sleep(0.01)
```

### 셀 출력 숨기기

셀 왼쪽의 출력 영역을 더블클릭하면 출력을 접을 수 있습니다.

### 폼(Form) 사용

```python
# @title 파라미터 입력 폼
name = "홍길동"  # @param {type:"string"}
age = 25  # @param {type:"slider", min:0, max:100, step:1}
activate = True  # @param {type:"boolean"}

print(f"이름: {name}, 나이: {age}, 활성화: {activate}")
```

## 12. 제한사항 및 주의사항

### 사용 제한

- **세션 시간**: 최대 12시간 (유휴 시 90분 후 자동 종료)
- **GPU 사용 시간**: 일일 제한 존재 (변동 가능)
- **RAM**: 약 12GB (무료 버전)
- **디스크**: 약 100GB (임시 저장소)

### 데이터 보존

- 런타임 종료 시 `/content` 디렉토리의 모든 데이터 삭제
- 중요한 데이터는 반드시 Google Drive에 저장
- 정기적으로 노트북을 저장할 것

### 모범 사례

1. 중요한 코드는 자주 저장하기
2. 긴 작업은 중간 결과를 Drive에 저장
3. GPU가 필요한 부분만 GPU 사용
4. 사용하지 않을 때는 런타임 연결 해제
5. 협업 시 버전 관리에 주의

## 13. Colab Pro/Pro+ 비교

| 기능 | 무료 | Pro | Pro+ |
|------|------|-----|------|
| RAM | ~12GB | ~25GB | ~50GB |
| GPU | 제한적 | 우선 접근 | 최고 GPU 접근 |
| 세션 시간 | 12시간 | 24시간 | 24시간 |
| 백그라운드 실행 | 불가 | 가능 | 가능 |

## 14. 추가 리소스

- **공식 문서**: [colab.research.google.com/notebooks/intro.ipynb](https://colab.research.google.com/notebooks/intro.ipynb)
- **튜토리얼**: Colab 메뉴 > 도움말 > FAQ
- **커뮤니티**: Stack Overflow, GitHub, Reddit

---

이제 Google Colab을 효과적으로 사용할 준비가 되었습니다! 실습을 통해 더 익숙해지시길 바랍니다.
