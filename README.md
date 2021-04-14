# Anomaly_Detection

## Anomaly Detection 종류 (학습데이터에 따라)
1. Supervised Anomaly Detection
   - 정상 sample과 비정상 sample의 Data와 Label이 모두 존재하는 경우
   - pros : 양/불 판정 정확도가 높다.
   - cons: 비정상 sample을 취득하는데 시간과 비용이 많이 든다. Class-Imbalance 문제를 해결해야 한다.
2. Semi-supervised Anomaly Detection
   - 정상 sample만 이용해서 모델을 학습하는 경우
   - method : One-Class SVM & Deep SVDD
   - pros : 비교적 활발하게 연구가 진행되고 있으며, 정상 sample만 있어도 학습이 가능하다.
   - cons : Supervised Anomaly Detection 방법론과 비교했을 때 상대적으로 양/불 판정 정확도가 떨어진다.
4. Unsupervised Anomaly Detection
   - 대부분의 데이터가 정상 sample이라는 가정을 하여 Label 취득 없이 학습을 시키는 경우
   - method : PCA & Auto-Encoder based Method 
   - pros : Labeling 과정이 필요하지 않다.
   - cons : 양/불 판정 정확도가 높지 않고 hyper parameter에 매우 민감하다.

![image](https://user-images.githubusercontent.com/67107675/114683454-0102c980-9d4b-11eb-9f95-01c5483bc9a8.png)


## Anomaly Detection 방법론
## Model-based Methods
### Isolation Forest 
- Tree based method로서 데이터를 분할 및 고립시켜 이상치를 탐지
### One-Class SVM 
- 데이터가 존재하는 영역을 정의하여, 영역 밖의 데이터들은 이상치로 간주

## Density/Distance-based Methods
### Gaussian Mixture Model
### k-Nearest Neighbours (kNN) method
### LOF(Local Outlier Factors)
- 데이터의 밀도 또는 거리 척도를 통해, majority 군집과 minority 군집을 생성하여 이상치를 탐지

## Reconstruction-based Methods
### PCA(Principal Component Analysis) Method
### Auto-Encoder based Method (ex. AAE(Adversarial Autoencoders))
- 고차원 데이터에서 주로 사용하는 방법론으로서 데이터를 압축/복원하여 복원된 정도로 이상치를 판단

- reference   
https://hoya012.github.io/blog/anomaly-detection-overview-1/
