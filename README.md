![image](https://user-images.githubusercontent.com/47529632/86557814-4f9c5f80-bf92-11ea-8670-5f481a467e00.png)

# SOMA Elastin


## Overview

![image](https://user-images.githubusercontent.com/47529632/86557885-94c09180-bf92-11ea-9477-d8423468bb33.png)


***“헤어샵에 가기 전 결과를 예측해볼 순 없을까?”***

&nbsp; 헤어샵 이용 고객들은 시술 결과를 마음에 들어 하지 않는 경우가 많다.
시술 결과가 예상과 다른 경우가 많기 때문이다. 시술 전 헤어 디자이너와 스타
일 상담을 하지만 의사소통이 제대로 되지 않는 경우가 많고, 시술 결과를 미리
볼 수 없기 때문에 불만족하는 것이다. 헤어 디자이너와 고객이 스타일 상담 시
효율적인 의사소통 수단이 필요하다는 생각이 들었다.

&nbsp; 비슷한 사진을 보여주는 것만으로 스타일 설명이 어렵고, 잘 어울릴지 시
술 전에 예측하기 힘들다. “헤어스타일 시뮬레이션”이 스타일 상담 시 효율적
인 의사소통 수단이 될 수 있을 것이다.

<br/>

<center><img src="https://user-images.githubusercontent.com/47529632/86558052-3647e300-bf93-11ea-8e3a-b69ceb77ebac.png"></center>

&nbsp; 사진 속 내 헤어스타일을 변경하는 시뮬레이션으로 헤어 시술 결과를 예
측해볼 수 있는 서비스를 제공한다. 다른 머리카락 그림을 단지 씌우는 것이 아닌 <U>내 머리스타일로부터의 수정</U>에 초점을 맞춘다. 사진 속 내 머리를 인식하고 헤어스타일을 수정한다. 헤어샵 방문 전 온라인으로 스타일 상담과 예약이 가능한 헤어샵 O2O 플랫폼으로 고객과 헤어디자이너 모두에게 도움을 준다.

⚫ 사진 속 “머리카락을 인식”한 스타일링 시뮬레이션
- 헤어 시술의 결과를 미리 볼 수 있고 헤어 디자이너는 스타일의 차이를 명확
하게 설명할 수 있다. 어떤 시술을 할지 결정할 수 있다.

⚫ 사용하기 “쉽지만 디테일한” 시뮬레이션
- 커트, 펌, 염색 등 다양한 스타일을 시뮬레이션할 수 있다. 높은 자유도로 디
테일한 시뮬레이션이 가능하며, 사용자가 사용하기 쉬운 인터페이스를 제공한다.

⚫ 헤어 디자이너와 고객을 연결하는 “플랫폼 서비스”
- 서비스를 통해 비대면 스타일 상담과 헤어샵 예약이 가능하다.
- 최근 미용업 시장 트렌드(개인화, 1인샵 증가)및 서비스 트렌드(O2O 플랫폼)


## 프로젝트 구조

1. HairNet (Deep Learning Network) [link](https://git.swmgit.org/swmaestro/elastin/tree/hairnet) [dev repo](https://github.com/eric-yoo/HairNet)
    - 딥러닝 기법을 활용해 2D 머리카락 이미지에서 3D 헤어 모델을 생성
2. HairNet Data Generation [link](https://github.com/eric-yoo/HairNet_DataSetGeneration)
    - HairNet의 딥러닝 네트워크 학습을 위한 데이터 생성
3. Hair, Face Segmentation [link](https://github.com/givenone/hair-segment)
    - HairNet의 딥러닝 네트워크 추론을 위한 데이터 전처리 모듈 1
4. HairNet Preprocessing [link](https://github.com/papagina/HairNet_orient2D) [dev repo](https://github.com/compass0/soma-experiment)
    - HairNet의 딥러닝 네트워크 추론을 위한 데이터 전처리 모듈 2
5. Hair Rendering [link](https://github.com/givenone/hair-renderer) 
    - HairNet의 딥러닝 네트워크 추론 결과 (3D hair model) 렌더링
6. 3D Face Reconstruction [link](https://github.com/givenone/face-recon)
    - eos 라이브러리를 활용한 3D face model 렌더링
7. Unity Application [link](https://git.swmgit.org/swmaestro/elastin/tree/unity)
    - 클라이언트 애플리케이션 (3D hair model 렌더링 및 편집)
8. Backend Server [link](https://git.swmgit.org/swmaestro/elastin/tree/server) [dev repo](https://git.swmgit.org/swmaestro/elastin/tree/server-dev)
    - 웹서버 및 딥러닝 엔진 (데이터 전처리 모듈 2개 및 HairNet 추론)
