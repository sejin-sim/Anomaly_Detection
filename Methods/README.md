## Model-based Methods
### Isolation Forest (unsupervised)
- Tree based method로서 데이터를 분할 및 고립시켜 이상치를 탐지
- feature를 랜덤하게 선택하고 선택한 feature의 최대값과 최소값의 사이 값을 분할함으로써 관측치들을 분리
- [Isolation forest IEEE 2008](https://arxiv.org/pdf/1811.02141.pdf) [[Code]](https://colab.research.google.com/github/sejin-sim/Anomaly_Detection/blob/main/Isolation_Forest.ipynb)   
![image](https://user-images.githubusercontent.com/67107675/114795087-cc355780-9dc8-11eb-9458-582164a8c5ed.png)

### One-Class SVM (unsupervised)
- 데이터가 존재하는 영역을 정의하여, 영역 밖의 데이터들은 이상치로 간주
- 엄연히 outlier-detection 방법 아니지만, novelty-detection method 이라고 할수는 있음   
  ㄴ training set은 outlier 에 의해서 오염되지 않아야 한다.
- [One-Class SVMs for Document Classification 2001](https://www.jmlr.org/papers/volume2/manevitz01a/manevitz01a.pdf) [[Code]](https://colab.research.google.com/github/sejin-sim/Anomaly_Detection/blob/main/One_class_SVM.ipynb)     
![image](https://user-images.githubusercontent.com/67107675/114798476-5fbe5680-9dd0-11eb-9098-52089ea9acff.png)

### Deep SVDD (semi-supervised)
- 딥러닝을 기반으로 학습한 데이터의 feature space를 통해 정상 데이터를 둘러싸는 가장 작은 구를 찾는 것이 목적
- 장점: 정상 sample만 있어도 학습이 가능
- 단점: Supervised Anomaly Detection과 비교했을 시, 상대적으로 양/불 판정 정확도가 떨어짐
- [Deep One-Class Classification ICML 2018](http://data.bit.uni-bonn.de/publications/ICML2018.pdf)  [[Code]](https://colab.research.google.com/github/sejin-sim/Anomaly_Detection/blob/main/Deep_SVDD_Pytorch.ipynb)        
![image](https://user-images.githubusercontent.com/67107675/114795830-7e215380-9dca-11eb-9068-58c7ef4c39c2.png)


## Density/Distance-based Methods
### Deep Autoencoding Gaussian Mixture Model(DAGMM)
- DAGMM : autoencoder + GMM으로 정보 유지(Key information) 및 밀도 추정에 강력한 성능을 보인다. 저차원으로 사영시킨뒤 GMM이용하여 각 군집의 밀도 함수를 추정 & 중심으로부터 거리가 먼 자료를 이상치로 탐지. 압축 네트워크(Compression network)와 추정 네트워크(Estimation network)로 이뤄져 있다. 게임 회사 어뷰징에 활용 되는 것을 확인함
 > 1) 압축 네트워크 : autoencoder 사용하여 입력 데이터의 차원을 축소
 > 2) 추정 네트워크 : 1)의 축소된 데이터를 입력값으로 사용하여 GMM으로 밀도를 추정 (k 설정 필요)
- [Deep Autoencoding Gaussian Mixture Model for Unsupervised Anomaly Detection ICLR 2018](https://sites.cs.ucsb.edu/~bzong/doc/iclr18-dagmm.pdf)  [[Code]](https://colab.research.google.com/github/sejin-sim/Anomaly_Detection/blob/main/DAGMM_Pytorch.ipynb)        
![image](https://user-images.githubusercontent.com/67107675/118203432-0ad93300-b497-11eb-8785-aaf1a4ce9846.png)

## k-Nearest Neighbours (kNN) method
### LOF(Local Outlier Factors)
- LOF : 데이터의 밀도 또는 거리 척도를 통해, majority 군집과 minority 군집을 생성하여 이상치를 탐지. 관측치의 주변 데이터(neighbor)를 이용하여 국소적(local) 관점으로 이상치 정도를 파악하는 것.
- pros : 집된 클러스터에서 조금만 떨어져 있어도 이상치로 탐지해준다. 밀집된 곳에 가까운 이상치들은 높은 LOF score를 가진다.
- cons : 이상치 판단 기준을 정해줘야 한다. 차원이 늘어나면 어렵다.
- [LOF: identifying density-based local outliers ACM 2000](https://dl.acm.org/doi/10.1145/342009.335388)  [[Code]](https://colab.research.google.com/github/sejin-sim/Anomaly_Detection/blob/main/LOF.ipynb)   
![image](https://user-images.githubusercontent.com/67107675/118427317-e0da7780-b707-11eb-8412-afbabf92f598.png)


## Reconstruction-based Methods
- 이상을 판별할 데이터를 저차원 형태의 잠재 구조(latent structure)를 획득하고, 그 이후 인위적으로 재구성한 데이터를 생성 위한 모델 사용
### PCA(Principal Component Analysis)
- 선형 재구성으로 제한되며 상관 관계가 높고 가우스를 따르는 데이터 분포에만 적용 가능하다는 한계가 있음 [[Code]](https://colab.research.google.com/github/sejin-sim/Anomaly_Detection/blob/main/PCA.ipynb)   
&nbsp; <img src="https://user-images.githubusercontent.com/67107675/122353725-4a5dd800-cf8b-11eb-8d2f-74b7364914ab.png" width = "50%">

## Auto-Encoder based Method 
<img src = "https://user-images.githubusercontent.com/67107675/126440633-0dd0dd88-a8d3-42f3-8a5a-ab70ea76bc35.png" width="40%">

### VAE(Variational Autoencoders)
![image](https://user-images.githubusercontent.com/67107675/126440804-89bec54d-f9ee-4127-aae2-86db3ffed5f6.png)

### AAE(Adversarial Autoencoders)
- VAE(Variational AutoEncoder) + GAN : latent distribution(잠재 분포) 검사하는 판별기(discriminator)를 도입하여 원하는 형태의 latent distribution(잠재 분포) 을 좀더 엄격하게 강제 가능

### RaPP(Reconstruction along Projection Pathway)
