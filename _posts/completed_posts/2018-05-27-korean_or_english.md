---
title: 한글/영어 텍스트 구분하기 
category: python-basic
tags: python python-basic nlp 
---

## 입력받는 텍스트는 어떤 언어인가? 

- 입력받는 텍스트가 모두 '한글'이거나 '영어'라면 좋겠지만, 그렇지 않습니다. 또, 한글과 영어가 섞여 있는 경우도 아주 많죠. 기술분야의 전문적인 용어의 경우는 더욱 영어일 가능성이 높아서, 명사는 영어로 작성되고, 조사/동사만 한글로 작성되는 경우가 매우 많습니다. 
- 아무튼, 그렇기 때문에, 텍스트가 한글인지, 영어인지를 구분하는 간단한 코드를 만들었습니다. 처음에는 어려울 줄 알았는데 작성해보니, 매우 간단하고 쉽네요. 

### code 

- 입력받은 문자열의 문자를 하나씩 읽으면서 해당 문자가 한글인지 영어인지를 카운트합니다. 한글이 하나라고 있을 경우에는, 한글로 간주합니다. 
- 이 부분이 클리어하지 않을 수도 있지만, 1) 한국 사람이 명사 등을 영어로 작성하는 경우는 있지만(사실 이는 한국어라고 보는 것이 타당하죠), 2) 한글만 명사로 작성되고 전체 맥락(동사 조사)는 영어로 작성되는 경우는 잘 없습니다. 그래서 그냥 한글이 하나라도 있는 경우 한글이다 라고 처리하는 것이 훨씬 깔끔합니다. 

```python
def isEnglishOrKorean(input_s):
    k_count = 0
    e_count = 0
    for c in input_s:
        if ord('가') <= ord(c) <= ord('힣'):
            k_count+=1
        elif ord('a') <= ord(c.lower()) <= ord('z'):
            e_count+=1
    return "k" if k_count>1 else "e"
```