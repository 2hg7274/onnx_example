# 들어가며...  
ML을 공부할 때는 scikit-learn, xgboost, catboost 등과 같은 패키지만 썼던 것 같다. 
그런데 DL에서는 주로 PyTorch, Tensorflow가 양대 산맥을 이루는 것 같다.
PyTorch 프레임워크로 개발한 모델을, Tensorflow 프레임워크로 개발한 모델을 서로 다른 프레임워크끼리 호환이 안된다. 
논문에서 발표한 모델을 써봐야지하고 github가서 학습된 모델을 다운받아서 써보려고 했는데 Tensorflow만 능숙한 사람이라면 무작정 써보기가 어려운 상황이 생긴다. (보통 github에 공개되는 모델들은 PyTorch로 개발된 모델들이 주로...)

이런 어려운 상황을 쉽게 도와주는 것이 ONNX라고 할 수 있다. 
***
# ONNX
![ONNX Image](https://velog.velcdn.com/images/2hg/post/76f99d5c-e2aa-4167-b1c5-2655620257d5/image.png)  

## Overview
신경망을 사용한 딥 러닝은 데이터 흐름 그래프에 대한 계산을 통해 수행된다. **일부 프레임워크(ex: Caffe2, Tensorflow)는 정적 그래프**를 사용하는 반면 **다른 프레임워크(ex: Pytorch, Chainer)는 동적 그래프**를  사용한다. 그러나 모두 개발자가 계산 그래프를 간단하게 구성할 수 있는 인터페이스와 그래프를 최적화된 방식으로 처리하는 런타임을 제공한다. 그래프를 개발자 소스 코드의 특정 의도를 포착하는 **Intermediate Representation(IR)** 역할을 하며, 특정 장치(CPU, GPU, FPGA 등)에서 실행되도록 최적화 및 변환하는 데 도움이 된다. 

## Why a common IR?
오늘날 각 프레임워크에는 그래프에 대한 고유한 표현이 있찌만 모두 유사한 기능을 제공한다. 즉, 각 프레임워크는 API, 그래프 및 런타임의 고립된 스택이다. 또한 프레임워크는 일반적으로 빠른 훈련, 복잡한 네트워크 아키텍처 지원, 모바일 장치에서의 추론 등과 같은 일부 특성에 최적화되어 있다. 이러한 특성 중 **하나에 최적화된 프레임워크를 선택하는 것은 개발자의 몫**이다. 또한 이러한 최적화는 특정 개발 단계에 더 적합할 수 있다. 이로 인해 전환의 필요성으로 인새 연구와 생산 사이에 상당한 지연이 발생한다.  

democratizing AI를 목표로 우리는 개발자가 개발 또는 배포의 모든 단계에서 자신의 프로젝트에 가장 적합한 프레임워크를 선택할 수 있도록 지원하는 것을 구상한다. ONNX(Open Neural Network Exchange) 형식은 이 강력한 생태계를 구축하는 데 도움이 되는 일반적인 IR이다.  

ONNX는 계산 그래프의 공통 표현을 제공함으로써 개발자가 작업에 적합한 프레임워크를 선택할 수 있도록 돕고, 작성자는 혁신적인 개선 사항에 집중할 수 있으며, 하드웨어 공급업체는 플랫폼 최적화를 간소화할 수 있다.  


## ONNX Runtime
![ONNX Runtime](https://velog.velcdn.com/images/2hg/post/9ef384d5-1c1d-448c-9ca2-281212d6bf26/image.png)  

ONNX Runtime은 다양한 플랫폼과 프레임워크에서 DNN의 추론과 학습을 가속시키기 위한 고성능 배포 엔진으로 소개되고 있다. 기본적으로 ONNX 형식의 모델을 사용하며, PyTorch, TensorFlow 등 기존의 메이저한 프레임워크들과도 문제없이 호환된다고 한다.

## PyTorch to ONNX example
PyTorch 튜토리얼에 PyTorch 모델을 ONNX로 변환하고 ONNX Runtime에서 실행해보는 코드가 있다. 같이 따라해보며 익혀보는 것도 좋을 것 같다.  
참고 링크는 다음과 같다. ([PyTorch to ONNX](https://github.com/2hg7274/onnx_example))

***  

# 참고 사이트  
[ONNX documentation](https://onnx.ai/onnx/)  
[ONNX Runtime documentation](https://onnxruntime.ai/docs/)
