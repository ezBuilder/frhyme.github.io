---
title: bash_profile을 정리합니다. 
category: others
tags: shell bash bash_profile
---

## bash_profile...

- conda에 문제가 생겨서 파이썬을 하나하나 다시 설치했는데, 그 과정에서 좀 문제가 생겼습니다. 몇가지 설정을 바꾸어야 할 것 같았는데, 그러다보니 bash_profile을 건드려야 하더라구요. 
- bash_profile에 뭔가 작성되어 있는데, 저는 정작 bash가 무엇인지도, bash_profile이 뭔지도 잘 몰라요. 그래서 이참에 잘 정리하면 좋을 것 같아서 씁니다. 

## bash??

- 제가 학부 전공이 컴퓨터가 아니라서, 운영체제니 쉘이니 이런걸 정말 몰라요. 다만 대략 찾아보니, bash란 약간 이런것 같아요. 

> 운영 체제 에서 이용자(나)와 커널(운영체제 내에서 프로세스를 관리하는 부분) 사이를 연결해주는 것

- 쉽게 말하면, 내가 '뭘 좀 해줘'라고 말하면, 그것을 해석해서 커널에 전달하는 느낌이라고 생각해도 되겠네요. 
- 일반적으로 쉘이라고 하면, GUI가 아니라 CLI를 뜻하는 것 같은데, bash는 (Bourne-again shell)의 약자로, 예전에 만들어준 쉘의 업그레이드 판인것 같네요. 

## bash_profile?

- 네 솔직히 저도 약간 제가 무슨 말하는지 모르겠는데, 커맨드라인 윈도우 같은거라고 마음대로 생각하려고요. 
- 아무튼, 쉘에서 프로그램을 막 설치하는건 문제가 아닌데, 지울때는 꼭, `.bash_profile`에 path를 지우라는 말들을 많이 하더라고요. 왜 그런지는 잘 모르겠는데, 아무튼 그래서, 내부에 뭐가 적혀 있는지 봤습니다. 

```bash
# added by Anaconda3 5.2.0 installer
export PATH="/Users/frhyme/anaconda3/bin:$PATH"
```

- 제가 다운받은, anaconda3가 주석과 함께 저기 잘 정리되어 있군요. 잘 모르겠지만, 무슨 path를 export해주겠다는 건데...흠
- 잘 모르니까. `/Users/frhyme/anaconda3/`로 들어가 보겠습니다. 

- 들어가서 보면, 이런저런 파일들이 많습니다. 폴더는 없고, 전부 파일들인데, 이상하게 이름이 낯설지 않아요. 그래서 개별 파일들을 그냥 커맨드라인에서 쳐보니까 되네요???

## 깨달음

- 약간, 이런것 같습니다. 

- `.bash_profile`은 일종의 설정 파일인데, 제가 쉘에서 뭔가를 실행하거나 할때, 특히 커맨드 라인에서 무언가를 칠 때(예를 들면 `conda` 등) 그 커맨드를 읽어오는 설정파일인 것 같아요. 따라서 파일에 `path`가 설정되어 있어야, 문제없이 커맨드라인에서 실행할 수 있는....뭐 그런거 아닐까요??
    - 제가 많이 쓰는 `conda`, 아니면 듣도 보도 못한, `h5fc` 등을 직접 커맨드라인에서 실행할 수있습니다. 

## wrap-up

- 맞는지 아리까리한데.....맞겠져...뭐.......