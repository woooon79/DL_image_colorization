# Hint-based image colorization with Unet

![image](https://user-images.githubusercontent.com/75998991/143178910-e05c7560-5c80-4699-95b0-e25ea6a307c0.png)

### Introduction
옛날 사진들은 대부분 흑백이며 화질이 선명하지 못한 경우가 많다. 많은 사람들이 이러한 사
진으로 이전 시대의 모습을 추측하기도 하고, 생생하게 보고 싶어 한다. 이를 위해 흑백 이미지
의 원래 색상을 추측해서 컬러로 볼 수 있게 해주는 컬러화 작업이 필요하다. 이번 연구에서는 
흑백이미지의 컬러화를 위해 다양한 CNN 기반의 딥러닝 모델을 사용하여 컬러 힌트를 기반으
로 새로운 컬러이미지를 생성하였다. 이번 연구를 통해 다양한 U-Net 구조의 딥러닝 모델을 컬러화 작업에 적용시켜보면서, 기본 Unet 
구조를 사용했을 때 보다 자연스럽고 높은 해상도와 고품질의 컬러화 된 이미지 결과를 얻을 수 있
었다. 향후에는 더 많은 dataset을 사용하고 다양한 hyperparameter들을 조절하면서 학습을 개선
할 것이고, 여기에 다양한 high-level의 feature를 세밀하게 추출하는 발전된 모델을 적용한다면 성능은 더욱 더 향상 될 것으로 기대한다


# Dataset
Training dataset과 Validation dataset은 Place365 와 ImagNet training dataset에서 무작위로 샘플링
하였다. 256 * 256 사이즈의 모든 이미지를 128 * 128 사이즈로 변경한 뒤 학습을 진행하였고, test 또한 
128 * 128 사이즈의 이미지가 적용되었다. 모든 dataset의 color-hint image는 원본이미지의 1%,3%,5% 
color를 랜덤으로 추출하여 생성하였다.

# Training and Evaluation
- Basic Unet
- Nested Unet
- Attention Unet
- **Nested attention Unet**

이번 실험에서는 Optuna framework를 이용하여 hyperparameter를 조절하였다. Optuna framework는 
사용자가 지정한 parameter들을 최적화하는 방향으로 자동으로 조합하여, 최적의 parameter 조합들을 
dataframe 형식으로 반환해준다. 
![image](https://user-images.githubusercontent.com/75998991/143179340-36a6ab61-30e0-4c5c-9085-67136bac9131.png)

# Result
![image](https://user-images.githubusercontent.com/75998991/143179415-cc7aeb60-2c51-4e10-b973-6e905b24c50b.png)  
기존의 Basic Unet, Attention Unet, Nested Unet으로 학습을 진행해본 뒤 Nested Unet에 attention 
block을 더한 Nested-Attention Unet 이라는 새로운 모델을 구성해보았다. 성능을 PSNR과 SSIM으로 
측정한 결과, Nested-Attention Unet>Nested Unet>Attention Unet>Basic Unet 순으로 
Nested-Attention Unet의 성능이 가장 좋았다.
