---
title: "📂 모델별 폴더 구조 가이드"
excerpt: "ResNet과 YOLO 모델 학습에 필요한 폴더 구조와 라벨 형식을 비교 정리한 자료입니다."
categories:
    - deep_learning
tags: [dataset, labeling, directory]
layout: single
header      :
  image     : /assets/images/2025/DLplanning/directory-structure.png
  overlay_color: "#222"
  overlay_filter: 0.1
  show_overlay_excerpt: true
  caption: "출처: [Kaggle - DAGM 2007 Optical Inspection Dataset](https://www.kaggle.com/datasets/mhskjelvareid/dagm-2007-competition-dataset-optical-inspection)"
toc: true
toc_label: "Contents"
permalink: /planning/data-structure-guidelines/
---

## 📌 개요

딥러닝 모델 학습은 대부분 정답이 주어진 **지도 학습(Supervised Learning)** 방식이다.  
즉, 학습 전에 사람이 이미지가 **정상인지, 결함이 있는지**를 먼저 지정해 줘야 한다.  
그리고 **모델별로 요구하는 폴더 구조와 라벨 포맷이 다르다.**

이번 포스트에서는 대표적인 분류 모델인 **ResNet**과  
대표적인 검출 모델인 **YOLOv5**를 기준으로  
각 모델이 요구하는 **디렉토리 구조와 라벨 형식**을 비교 정리했다.


---

### ✅ 모델별 데이터 구성 비교

| 모델 유형 | 예시 모델 | 디렉토리 구조 | 라벨링 방식 |
| --- | --- | --- | --- |
| 🧠 분류 (Classification) | `ResNet` | `data/defect/`, `data/normal/` | 폴더명이 곧 라벨 (`ImageFolder` 방식) |
| 📍 검출 (Detection) | `YOLOv5` | `images/train/`, `labels/train/` + `.txt` or `label.csv` | 바운딩 박스 좌표 + 클래스 번호 필요
(`x,y,w,h,class`) |

---

### 🧪 예시 1: 분류 모델 (ResNet)

```
data/
├── defect/
│   ├── 001.png
│   └── ...
├── normal/
│   ├── 001.png
│   └── ...
```

- [Resnet 구조의 2007 DAGM]()
- Resnet의 폴더 구조는 정상 폴더와 결함 폴더 두 가지로 나뉘어있다.
- 간단한 구조이지만 반드시 둘 다 있어야 학습이 가능하다. 
- 대신 별도의 라벨 파일 없이도 학습이 가능하다.

### 🧪 예시 2: 검출 모델 (YOLO)

```
datasets/
├── images/
│   ├── train/
│   ├── val/
├── labels/
│   ├── train/
│   ├── val/
```

- [YOLO 구조의 2007 DAGM](https://www.kaggle.com/datasets/mhskjelvareid/dagm-2007-competition-dataset-optical-inspection)
- 각 이미지에 대응하는 라벨 파일 (`.txt`) 혹은 `label.csv` 파일이 필요하다.
- 라벨은 결함의 위치와 크기 정보가 들어있는 텍스트 파일이다.
- YOLO 라벨 예시 (`labels/train/0001.txt`)
    
    ```css
    # class x_center y_center width height
          0    0.45   0.52     0.2     0.1  
    ```
    
- 보통 **비율(0~1)**로 표현하지만,
- 일부는 **절대값(px)**를 사용한다.
- 같은 데이터셋이라도 폴더 구조가 다르므로 라벨 설명을 읽는 것이 낫다.
-  


### 🔢 파일 이름 짓기 팁

이미지 파일 이름은 `1`, `23`, `456`보다

`0001`, `0023`, `0456`처럼 **자릿수를 맞춰 정렬**하는 것이 안전하다.

- 정렬 오류를 방지할 수 있다.

{: .notice--tip}

