[logo]

# SOMA Elastin


## Introduction

***“헤어샵에 가기 전 결과를 예측해볼 순 없을까?”***

- 헤어샵 이용 고객 중에는 시술 결과가 예상과 달라 결과를 마음에 들어 하지 않는 사람이 많다. <br>
  - 시술 전 헤어 디자이너와 스타일 상담을 하지만 의사소통이 제대로 되지 않는 경우가 많고, 시술 결과를 미리 볼 수 없어서 불만족한 것이다. <br>
  - 본 프로젝트는 헤어 디자이너와 고객이 스타일 상담 시 효율적인 의사소통 수단이 부족하다는 발상에서 출발한다. 

- 헤어샵에서 고객은 자신이 원하는 스타일의 사진을 보여주는 것만으로는 스타일 설명이 어렵다
  - 의사 소통 수단의 부재로 어떤 스타일이 자신과 잘 어울릴지 시술 전에 예측하기 힘들다. 
  - 사실적이고 자유도 높은 “헤어스타일 시뮬레이션”을 통해 효율적인 스타일 상담이 가능할 것이다.


- 사진 속 내 헤어스타일을 변경하는 시뮬레이션으로 헤어 시술 결과를 예측해볼 수 있는 서비스를 제공한다. 
  - 단순히 다른 머리카락 그림을 씌우는 것이 아닌 <U>내 머리스타일로부터의 수정</U>에 초점을 맞춘다.
  - 사진 속 내 머리를 인식하고 헤어스타일을 수정할 수 있어 헤어샵 방문 전 시뮬레이션이 가능하다.
  - 온라인으로 스타일 상담과 예약이 가능한 헤어샵 O2O 플랫폼으로 고객과 헤어디자이너 모두에게 도움이 될 수 있다.


## Overview

- 사진 속 인물의 머리카락을 감지해 3D 복원 및 스타일링 시뮬레이션
    - 사진의 실제 머리카락 가닥을 인식하여 더욱 현실적이고 자연스러운 결과를 제공
    - 현실감 있는 시뮬레이션으로 고객에게 개인 맞춤형 서비스를 제공

- 전문가와의 인터뷰를 통해 사용자 친화적인 시뮬레이션 인터페이스 구현
    - 실제 헤어 디자이너가 스타일 상담에 필요한 다양한 기능 제공
    - 커트/펌/염색 등 다양한 헤어스타일의 시뮬레이션이 가능하도록 함
    - 3D 시뮬레이션으로 모든 스타일을 시뮬레이션하고, 다양한 각도에서 시술 결과를 예측해 볼 수 있음 

- 헤어 시술 전 스타일 체험을 통해 미용사와 고객을 연결하는 서비스
    - 헤어샵 충성고객 확보를 위한 차별화된 프리미엄 서비스
    - 미용사와 고객 간 비대면 스타일 상담 등에 활용돼 고객 만족도 증진
    - 최근 미용업 시장 트렌드(개인화, 1인샵 증가) 및 연관 서비스 트렌드(O2O 플랫폼 등장 e.g. 카카오헤어)에 부합


## Technology

- Computer Vision & Deep Learning
    - 인물 이미지에서 얼굴과 머리카락, 그리고 배경에 해당하는 영역을 구분하기 위해 딥러닝으로 Semantic Segmentation 모듈을 개발하고 학습했다. ResNet 기반 심층 신경망인 PSPNet을 사용했다.  PSPNet Pyramid Scene Parsing Network (Hengshuang Zhao et al, CVPR 2017)
    - 얼굴 이미지를 3D 모델로 복원하기 위해 얼굴의 특징점(face landmark)을 검출하며, 이를 위해 오픈소스 딥러닝 라이브러리인 dlib을 사용했다. 이후 eos 라이브러리를 사용해 특징점들을 기준으로 얼굴 texture를 추출 후 3D morphable model에 fitting하여 3D face 모델을 생성했다.  Fitting a 3D Morphable Model to Edges: A Comparison Between Hard and Soft Correspondences(Anil Bas et al, ACCVW 2016)
    - 2D 이미지의 머리카락 영역에 Gabor Filter 등의 영상처리 기술을 사용해 머릿결 정보를 추출하였다. 이를 사용해 3D 머리카락 데이터를 생성하기 위해 두 가지 딥러닝 기반 기법을 구현하고 학습했다. https://github.com/papagina/HairNet_orient2D
    - 3D 헤어 모델과 그것의 2D 렌더링 결과(머릿결 이미지)를 지도 학습시키는 방법(HairNet)을 구현하고 학습을 진행했다. 학습이 완료된 후에는 2D 머릿결 이미지를 입력으로 네트워크가 3D 헤어 모델을 생성한다. HairNet: Single-View Hair Reconstruction using Convolutional Neural Networks(Yi Zhou et al, ECCV 2018)
    - 머릿결 이미지들을 CNN 네트워크로 인코딩하여 상호 유사도를 비지도 학습으로 계산하는 네트워크를 학습했다. 2D 머릿결 이미지를 입력하면 가장 높은 유사도로 렌더링되는 3D 헤어 모델을 추천한다. 딥러닝의 구현과 학습을 위해 최신 ICML 논문 등을 참고했다. A Simple Framework for Contrastive Learning of Visual Representations (ICML 2020, Ting Chen et al.)


- 3D Computer Graphics
    - 3D 헤어 모델과 얼굴 데이터를 자연스럽게 렌더링하고 시뮬레이션을 하기 위해 Unity를 사용해 3D 어플리케이션을 개발했다. 머리카락을 빠르고 자연스럽게 렌더링하기 위해서 셰이더를 구현했다.
    - 3차원 vertex들의 위치와 Curvature를 조작하여 다양한 헤어 시술을 독창적으로 구현했다. 머리카락 선택, 커트, 펌, 염색 등을 구현했으며 레이어드 컷, C컬, S컬 등을 구현했다. 각 머리카락을 trigonal function으로 근사하여 3D 변환을 적용하고. Spline, Ray tracing 등의 기술을 적용했다.


## Project Structure

- `master` 브랜치가 다른 브랜치들을 submodule 형태로 tracking한다.<br>
크게는 딥러닝 및 앱 서버 구현체 (server) / 유니티 클라이언트 구현체 (unity)로 구분되며 각 브랜치에 상세되어 있다.

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
    - 웹서버 및 딥러닝 엔진 (데이터 전처리 모듈 2개 통합 및 HairNet 추론)


## Demo
1. Screenshots

2. Video Clips


## Reference & Acknowledgement

1. 설문 및 인터뷰 자료
- 두잇 서베이 https :://doooit tistory com/ 679
- 그라피언 인터뷰 https :://www e graphy co kr/news/articleView html?idxno= 5703
- “차홍 뷰티 전문가 인터뷰 영상 https :://www youtube com/watch?v=WVIssx 68 VHw

2. 논문
- PSPNet: Pyramid Scene Parsing Network (Hengshuang Zhao et al, CVPR 2017)
- Fitting a 3 D Morphable Model to Edges A Comparison Between Hard and Soft Correspondences(Anil Bas et al, ACCVW 2016)
- HairNet Single View Hair Reconstruction using Convolutional Neural Networks(Yi Zhou et al, ECCV 2018)
- A Simple Framework for Contrastive Learning of Visual Representations (Ting Chen et al, ICML 2020)
- Practical Real Time Hair Rendering and Shading (Thorsten Scheuermann et al, SIGGRAPH 2004)
