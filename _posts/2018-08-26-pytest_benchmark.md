---
title: pytest-benchmark 사용하기 
category: python-lib
tags: python python-lib pytest test benchmark jupyter-notebook
---

## 두 함수의 성능 비교하기. 

- 코딩을 하다가 성능을 테스트할 일들이 종종 있잖아요. 예를 들어서 이 부분이 좀 느린 것 같은데 정말 그런가? 뭐 그렇게 테스트 할 일들이 있습니다. 그냥 귀찮아서 보통은 다음으로 간단하게 처리할 때도 많죠 

```python
import time 

start_time = time.time()
## compare code 
print(time.time() = start_time)
```

- 그런데 이건 아무래도 별로죠. 그때 상황의 변수가 일정하게 반영되지 않고, 평균값등으로 찾아주는 것도 아니고요. 

## pytest-benchmark

- 다른 사람들 코드를 보다보면 속도를 비교할때 보통 pytest-benchmark를 사용하더라구요. 그래서 저도 한 번 사용해봤습니다. 
- 일단 설치부터 하구요. 

```
pip install pytest-benchmark
```

- 코드는 다음처럼 작성되어야 합니다. 
    - 일단 해당 파일에 함수 두개를 작성하고, 
    - `benchmark`를 input으로 받고, 내부에는 `benchmark(<func_name>, argument)`만 작성되어 있는 함수를 각각 만들어둡니다. 

```python
import numpy as np

## 성능을 비교할 함수 1
def func1(s=10000):
    a = np.array([i for i in range(0, s)])
    return a.mean()
## 성능을 비교할 함수 2
def func2(s=10000):
    a = [i for i in range(0, s)]
    return sum(a)/len(a)
##############################
## 함수1을 테스트할 함수 
def test_func1(benchmark):
    benchmark(func1, 10000)
## 함수2를 테스트할 함수 
def test_func2(benchmark):
    benchmark(func2, 10000)
~
```

- 이렇게 만든 파일의 이름이 예를 들어 `a.py`라고 하면 터미널에서 아래 커맨드를 수행합니다. 

```bash
pytest --benchmark-only a.py
```

- 그럼 아래와 같이 시간 등이 비교된 결과가 도출됩니다. 

```
a.py ..                                                                                                                                                                    [100%]


----------------------------------------------------------------------------------------- benchmark: 2 tests -----------------------------------------------------------------------------------------
Name (time in us)            Min                   Max                  Mean             StdDev                Median                IQR            Outliers         OPS            Rounds  Iterations
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
test_func2              528.2880 (1.0)      1,284.6999 (1.0)        556.4796 (1.0)      30.9150 (1.0)        550.1145 (1.0)       8.2795 (1.0)       124;305  1,797.0110 (1.0)        1732           1
test_func1            1,114.0830 (2.11)     1,684.9340 (1.31)     1,143.8775 (2.06)     61.7504 (2.00)     1,124.2030 (2.04)     25.1330 (3.04)        38;56    874.2195 (0.49)        571           1
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

```


## jupyter notebook에서 pytest 하기 

- 다 좋은데 커맨드 라인이랑 왔다갔다 하는게 귀찮을 수 있습니다. 
- 또 보통 한 파일에 저렇게 함수만 딱 두는 경우는 잘 없으니까요. 그래서 jupyter notebook에서 사용할 수 있는지 확인해보려고 합니다. 

- 우선, pytest의 경우는 존재하는 파일에만 작용합니다. 따라서, 쥬피터 노트북의 특정 셀을 파일로 넘겨주는 커맨드가 필요하죠. 아래와 같이 사용하고 

```python
%%file test_a.py ## 현재 cell의 내용을 현재 디렉토리에 test_a.py 파일에 작성해줌 
import numpy as np

## 테스트할 함수를 만들어봄 
def func1(s):
    a = np.array([i for i in range(0, s)])
    return a.mean()
def func2(s):
    a = [i for i in range(0, s)]
    return sum(a)/len(a)

#assert func1(s)==func2(s)
def test_func1(benchmark):
    benchmark(func1, 10000000)
def test_func2(benchmark):
    benchmark(func2, 10000000)
```

- 그다음 셀에서 다음을 수행해줍니다. 

```bash
!pytest test_a.py
```

- 그럼 다음처럼 그 결과가 아주 잘 나옵니다. 좋군여 

```
test_a.py ..                                                             [100%]


---------------------------------------------------------------------------------------- benchmark: 2 tests ---------------------------------------------------------------------------------------
Name (time in ms)            Min                   Max                  Mean             StdDev                Median                 IQR            Outliers     OPS            Rounds  Iterations
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
test_func2              851.5339 (1.0)        877.4852 (1.0)        863.4813 (1.0)      10.8602 (1.0)        863.2845 (1.0)       18.6351 (1.0)           2;0  1.1581 (1.0)           5           1
test_func1            1,495.4562 (1.76)     1,698.4523 (1.94)     1,559.8910 (1.81)     85.7477 (7.90)     1,509.3657 (1.75)     111.0139 (5.96)          1;0  0.6411 (0.55)          5           1
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

```

## wrap-up

- 쥬피터 노트북에서 비교적 편하게 쓸 수 있으니까 좋은 것 같아요. 간단하게 코딩해서 테스트할 때 pytest를 이용하면 더 효과적으로 benchmark를 할 수 있을 것 같아요. 



## reference 

- <https://pytest-benchmark.readthedocs.io/en/latest/installation.html>