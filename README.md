# PatternRecognition_Term_2019Fall

Spatial Pyramid Matching을 이용해 Caltech 101을 Bag of visual words로 classification한 task입니다.


# Installation
  
colab 환경에서 opencv를 3.4.2.16버전으로 다운그레이드하여 사용했으며 
kmeans의 initialization을 gpu에서 하기 위해 kmc2 라이브러리를 사용하였습니다.

```bash
!yes | pip uninstall opencv-python
!yes | pip uninstall opencv-contrib-python
!yes | pip install opencv-python==3.4.2.16
!yes | pip install opencv-contrib-python==3.4.2.16
!pip install kmc2
```  

# Method
- Level0와 strong feature를 이용한 BOVW
(Level0_strongFeature.ipynb)
  1. 논문에 기재되어있는 대로 Caltech 101 dataset을 사용하였고 trainset은 각 class마다 30장씩 사용

  2. step==8 인 Dense SIFT를 사용하였고 이를 통해 descriptor를 추출

  3. Descriptor들을 kmeans 클러스터링을 이용해 200개의 codeword로 만든 뒤 각 descriptor를 비교하여 histogram을 쌓음

  4. 쌓은 histogram으로 svm classifier를 이용해 분류

- Level2와 strong feature를 이용한 BOVW (SPM level2)
(LevelPyramid_strongFeature_v2_word200.ipynb)

  1. Level0와 strong feature를 이용한 BOVW의 3번의 codeword로 만드는 것까지 동일하게 진행
  
  2. descriptor를 원래사이즈, 1/4사이즈, 1/16사이즈로 나눠서 histogram을 쌓음
  
  3. 쌓은 descriptor들의 gramMatrix를 구함
  
  4. 구한 gramMatrix로 svm classifier를 이용해 분류
  
- Level2와 strong feature를 이용한 BOVW (SPM level2) <- codeword = 600
(LevelPyramid_strongFeature_v2_word600.ipynb)

  1. Level2와 strong feature를 이용한 BOVW (SPM level2)와 동일하나 codeword만 600개로 늘려서 뽑음
  
  

# Result

| Name | codebook size | Result |
|---|---|---|
|Level0와 strong feature를 이용한 BOVW | 200 | 40.484% |
|Level2와 strong feature를 이용한 BOVW (SPM level2) | 200 | 58.333% |
| Level2와 strong feature를 이용한 BOVW (SPM level2) | 600 | 60.933% |
