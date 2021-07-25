# Normalizing Flow

## PAPER
- [NICE: Non-linear Independent Components Estimation(2014, Laurent Dinh, David Krueger, Yoshua Bengio)](https://arxiv.org/pdf/1410.8516.pdf)

### Prerequisites
- What is 'ICA(Independent Components Analysis, 독립성분분석)'?
    - reference : ['공돌이의 수학정리노트(독립성분분석(ICA)의 의미와 유도 과정 소개)'](https://youtu.be/HcMFFWcrE_U)
    - 독립성분분석은 중심극한정리를 거꾸로 생각하는 것

        [example]
        - 방에서 두 사람이 동시에 말을 하고 있다고 하자. 그리고 두 개의 마이크로 녹음을 진행하고 있다고 하자. 마이크로 녹음된 신호를 $\[x_{1}(t), \[x_{2}(t)$라고 하고, 두 사람의 음성신호를 $\s_{1}(t), \s_{2}(t)$라고 하면, 다음과 같이 모델링 할 수 있다.

        $$
        \[x_{1}(t)=a_{11}s_{1}(t)+a_{12}s_{2}(t), x_{2}(t)=a_{21}s_{1}(t)+a_{22}s_{2}(t)\]
        $$



        <img width="847" alt="스크린샷 2021-07-25 오전 11 40 17" src="https://user-images.githubusercontent.com/63832233/126885871-2252752f-607f-43c0-bf07-6693e327e47a.png">
    
        - 중심극한정리
            - 서로 독립적인 랜덤 변수(x)들의 선형조합 y ~ 가우시안 분포를 따름
                - y = Ax  <--> x = inv(A)y <--> x = Wy (W = inv(A))
            - 선형조합에 들어가는 독립변수들이 많을 수록 더욱 더 가우시안 분포에 가까워진다.
        - 독립성분분석
            - 선형조합을 통해 더 가우스분포에 가까운 분포를 따르는 결과물(x)들을 어떻게 조합하면 원래의 독립적인 source를 얻을 수 있을까?
            - ICA는 source들이 서로 독립적이라는 가정을 최대한 만족할 수 있도록 하는 W = inverse(A)를 찾는 것이 목적
        - 


### Summary
---
Paper proposed a deep learning framework for modeling complex hight-dimensional densities called Non-linear Independent Component Estimation(NICE).

