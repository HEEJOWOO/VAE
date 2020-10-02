# VAE : https://arxiv.org/abs/1312.6114

#### <I studied while referring to various sites, but it is not enough. Thanks anytime for feedback.>
### <heejo5@naver.com>

Auto-Encoding Variational Bayes
-------------------------------
![image](https://user-images.githubusercontent.com/61686244/94905051-347cb580-04d7-11eb-9afb-f36001cff5da.png)
* 기존 Auto Encoder의 구조는 위의 그림에서처럼 보이는 것 처럼 Encoder 와 Decoder 두 파트로 구성
* Encoder는 입련된 이미지의 정보를 압축하는 걸 담당하고 Decoder는 압축된 이미지의 정보를 사용하여 다시 복원시키걸 담당
* 어떤 입력에 대해서 특징을 추출하여 입력의 압축된 정보를 Latent Variables에 담고, 이 Latent Variables로부터 다시 자기 자신을 복화 하는 알고리즘
* Encoder는 정보를 압축하는데, Decoder를 통해 정보를 복원 하는데 사용
* 고차원 정보가 들어와 저차원에 정보를 압축하여 다식 고차원 공간으로 복원 시키는 구조

VAE 목적과 구성
--------------
![image](https://user-images.githubusercontent.com/61686244/94905281-96d5b600-04d7-11eb-9725-8b01d852ca6c.png)
* VAE는 생성 모델로 사용하기 위해 Sampling 과 확률적 개념을 집어넣은 것 
* VAE는 Generative Model 중 하나로, 확률분포를 학습함으로써, 데이터를 생성하는 것이 목적
* Encoder 네트워크는 학습용 데이터를 입력으로 받고 잠재 변수의 확률분포에 대한 파라미터를 출력
* Decoder는 잠재변수에 대한 확률 분포)에서 샘플링한 벡터를 입력받아, 이를 이용해 이미지를 복원
* 최종적으로 VAE의 학습 과정은 Encoder에 x가 입력 돼서 정규분포를 따르는 q파이를 거쳐 q(z|x) 분포가 구해집니다 후에 q(z|x)로부터 z 샘플링, Decoder에 대입하여 P(x|z)를 얻고 목적함수의 값을 구해 역전파를 통해 Encodr 의 파라메터 파이와 Decoder의 파라메터 세타를 업데이트 하는 방식으로 진행

변분추론(Variational Inference)
------------------------------
![image](https://user-images.githubusercontent.com/61686244/94905507-f0d67b80-04d7-11eb-9d1a-eb0b328e7b8d.png)

목점 함수(ELBO)
--------------
![image](https://user-images.githubusercontent.com/61686244/94905615-224f4700-04d8-11eb-8214-230afbb4a5dc.png)
![image](https://user-images.githubusercontent.com/61686244/94905852-76f2c200-04d8-11eb-87f7-22cfcca62132.png)

* KL-Divergence는 항상 0이상의 값을 갖는 다는 성질을 이용하여 목적함수의 하한 경계를 나타낼 수 있음
* 목적함수 ELBO의 하한선 식 5를 보게 되면 q와 p에 들어가는 입력값들이 앞에서 정의했던것처럼 둘 다 가우시안 분포를 따르기때문에, KL-Divergence에 들어가는 입력값이 정규분포를 따를때 간략화 할 수 있는 KL-Divergence의 성질에 의해 간략화 될 수 있음
* 목적함수의 하한선을 보게 되면 왼쪽에 보이는 기대값으로  표현한 식은 입력 x가 주어졌을 때 z가 encoder의 결과로 얻어진 분포를 따르고 다시 z일때 샘플 x가 생성될 학률의 기대값을 나타냄
* 즉 입력 데이터가 encoder를 통해 정규분포를 따르는 어떤 공간에 표현되고 이로부터 다시 decoder를 통과했을 때 x가 되게끔 하는 것을 목적으로 하는 것으로 Reconstruction Error를 의미
* Reconstuction Error은 AutoEncoder 관점에서 본 x에 대한 복원 오차이고 KL Divergence로 표현한 Regularization은 주어진 데이터로 부터 z를 잘 샘플링 했는지를 나타내는 척도를 나타냄
* KL-Divergence는 항상 0이상의 값을 갖는 다는 성질을 이용하여 목적함수의 하한 경계를 나타낼 수 있음
* 목적함수 ELBO의 하한선 식 5를 보게 되면 q와 p에 들어가는 입력값들이 앞에서 정의했던것처럼 둘 다 가우시안 분포를 따르기때문에, KL-Divergence에 들어가는 입력값이 정규분포를 따를때 간략화 할 수 있는 KL-Divergence의 성질에 의해 간략화 될 수 있음
* 계속해서 목적함수의 하한선을 보게 되면 왼쪽에 보이는 기대값으로  표현한 식은 입력 x가 주어졌을 때 z가 encoder의 결과로 얻어진 분포를 따르고 다시 z일때 샘플 x가 생성될 학률의 기대값을 나타냄
* 즉 입력 데이터가 encoder를 통해 정규분포를 따르는 어떤 공간에 표현되고 이로부터 다시 decoder를 통과했을 때 x가 되게끔 하는 것을 목적으로 하는 것으로 Reconstruction Error를 의미
* 즉 Reconstuction Error은 AutoEncoder 관점에서 본 x에 대한 복원 오차이고 KL Divergence로 표현한 Regularization은 주어진 데이터로 부터 z를 잘 샘플링 했는지를 나타내는 척도를 나냄

MNIST 데이터
-----------
![image](https://user-images.githubusercontent.com/61686244/94906014-bfaa7b00-04d8-11eb-8612-00a26d3e16b5.png)
![image](https://user-images.githubusercontent.com/61686244/94906040-c76a1f80-04d8-11eb-994e-714a9b52d4e6.png)

Conclusions
-----------
* 변분추론(Variational Inference)를 사용하여 기존 문제를 최적으로 바꿔줌
* Latent Space를 통해서 데이터의 군집을 파악하는데도 군집 강도가 높기 때문에 데이터의 특징을 파악하는데 유리
* 통계 기법을 추가하여 연속적이고 구조적인 잠재 공간을 학습하도록 만들었고 분포를 적용시켜 랜덤으로 추출함
* 안정성을 향상시키고 잠재 공간 어디서든 의미 있는 표현을 인코딩 하도록 만듬




