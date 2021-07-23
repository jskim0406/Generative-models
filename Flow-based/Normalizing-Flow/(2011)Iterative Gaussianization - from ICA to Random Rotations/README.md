# Normalizing Flow

## PAPER
- [Iterative Gaussianization: from ICA to Random Rotations(2011, Laparra et. al.)](https://arxiv.org/pdf/1602.00229.pdf)


### Motivation
---
> "Random sample x가 있을 때, x의 random variable 'X'의 분포(PDF)를 어떻게 추정할 수 있을 까?"

위와 같은 질문에 대한 답을 찾아나가는 과정에서 시작합니다.

Solution은 간단합니다. 

추정하고자 하는 unknown X의 분포를 우리가 알고 있는 Y의 분포로 변환(transformation)할 수 있습니다. 만약 이 변환이 가역적(invertible)이고, 미분가능(differentiable)하다면, 우리는 inverse pass를 통해 unknown X의 분포를 추정해낼 수 있을 것 입니다. 그리고 이 과정은 변수변환의 과정입니다. 

이 과정을 수식으로 표현하면 아래와 같습니다.

$$
p_{\mathbf{x}}(\mathbf{x})=p_{\mathbf{y}}(\mathcal{G}(\mathbf{x}))\left|\frac{d \mathcal{G}(\mathbf{x})}{d \mathbf{x}}\right|=p_{\mathbf{y}}(\mathcal{G}(\mathbf{x}))\left|\nabla_{\mathbf{x}} \mathcal{G}(\mathbf{x})\right|
$$

이 과정은 해석적으로 한번에 계산을 해내기 보단, iterative하게 단계 별로 나눠 접근하는 방법이 보다 적합하다고 논문에서 주장합니다.

이 Iterative transformation은 각각이 어떠한 목표를 갖고 있어야 할 것 입니다. 이는 일종의 'Loss function'을 통해 그 목표를 갖도록 디자인 할 수 있겠죠. 본 논문에선 그 Loss function으로 KL-divergence를 언급합니다. known PDF(PDF of Y)와 변환된 PDF가 서로 같도록 학습을 시켜줘야 하기에, 두 PDF 간 KL-divergence가 작아져야 할 것 입니다. 따라서, KL-divergence 가 두 PDF 간 최소화되도록 최적화 문제를 정의해 해결해 나갑니다. 이를 수식으로 표현하면 아래와 같습니다.

$$
J(x) = D_{KL}(p(x)|N(0,I))
$$



### Proposed method
---
- RBIG : Rotation-based Iterative Gaussianization
    
본 논문에서 제안하는 알고리즘 RBIG의 기본적인 구조는 아래와 같이 표현됩니다.

> "sequential application of a univariate marginal gaussianization transform followed by an orthonormal transform"

무슨 말일까요?

수식으로는 아래와 같이 표현됩니다.

$$
\mathcal{G}: \mathbf{x}^{(k+1)}=\mathbf{R}_{(k)} \cdot \mathbf{\Psi}_{(k)}\left(\mathbf{x}^{(k)}\right)
$$

매 iteration마다, 2-step process가 적용됩니다. 

1. Marginal Gaussianization

수식에선 $\mathbf{\Psi}_{(k)}\left(\mathbf{x}^{(k)}\right)$에 해당하는 부분입니다. unknown Random variable인 X를 Gaussianization을 먼저 진행합니다.

2. Rotation

Gaussianization된 X에 Rotation 연산 프로세스를 진행합니다. 수식에선 $\mathbf{R}_{(k)} $행렬이 내적 연산으로 이를 수행하게 됩니다.



## Conclusion
---
본 논문은 RBIG라는 PDF estimation 방법론을 제안했습니다. 이 알고리즘은 미분 가능한 iterative transformation 과정을 디자인했습니다. 이를 통해 iterative step 마다 unknown PDF를 계산해낼 수 있게 되었습니다. 결과적으로 이미지 합성, 이미지 분류, De-noising, multi-information estimation 에서 좋은 성능을 보여주었습니다. 




