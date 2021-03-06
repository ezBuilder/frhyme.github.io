---
title: 코덱과 컨테이너
category: others
tags: video format
---

## 코덱과 컨테이너

### 코덱

- 코덱은 COder and DECoder 를 말합니다. 
    - 간단히 얘기하면, 우리가 보통 사용하는 영상 파일들은 압축된 상태인데, 압축을 풀어야 (Decoding) 비디오를 볼 수 있습니다. 
    - 비슷하게, 우리가 영상을 mp4등의 파일로 저장하려면, 우리가 특정한 파일 포맷으로 encoding해야 비디오를 저장할 수 있구요. 
- 두 과정에 모두 관여하는 것이 바로 Encoder, Decoder이며, 이를 합쳐서 코덱이라고 부릅니다. 무손실 코덱도 있고, 손실 코덱도 있습니다. 
- 또한, 오디오와 비디오 각각에 관여하는 coder, decoder가 당연히 다릅니다. 예를 들어, 비디오는 출력이되나 오디오는 출력이 되지 않는 경우들이 있는데, 이러한 경우는 비디오 디코더는 있으나, 오디오 디코더는 없는 경우를 말합니다. 

### 컨테이너 

- 컨테이너란 일반적인 비디오 파일들을 말합니다. avi, mp4 등은 컨테이너 포맷을 말하구요.
- 특히, 비디오 파일에만 컨테이너라는 이름이 붙는데, 이미지/오디오와는 다르게 비디오는 이미지, 오디오 그리고 자막까지 서로 다른 종류의 데이터를 한데 묶어두는 것이 필요합니다. 이래서 컨테이너라는 이름이 따로 붙는 것이죠. 
- 각각의 컨테이너 포맷으로 변환하면, 이를 변환해주는 코덱이 있어야 재생시에 문제가 없겠죠. 

- 즉, 정리하면, 비디오파일은 컨테이너에 데이터가 있고, 이를 코덱을 이용해서 풀어서 재생하고, 압축해서 파일로 변환한다고 보면 될것 같습니다. 

## 코덱 more

- 코덱에 대해서 더 알아봅시다. 

## reference

- <https://www.motionelements.com/blog/ko/articles/what-you-need-to-know-about-the-5-most-common-video-file-formats>