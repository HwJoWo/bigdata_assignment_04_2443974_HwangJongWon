# 스트리밍 알고리즘 정확도·메모리 Trade-off 분석  
# Streaming Algorithms Trade-off Analysis

## 1. 프로젝트 개요 (Project Overview)

본 프로젝트는 대용량 데이터 스트림 환경에서 전체 데이터를 저장하지 않고 근사 계산을 수행하는 **스트리밍 알고리즘(Streaming Algorithm)** 을 구현하고, **정확도(Accuracy), 메모리 사용량(Memory Usage), 처리 시간(Processing Time)** 간의 Trade-off를 분석하는 것을 목표로 한다.

MovieLens 1M 데이터셋을 활용하여 다음 알고리즘을 직접 구현하고 비교 실험을 수행하였다.

This project aims to implement streaming algorithms for large-scale data stream processing and analyze the trade-off between **accuracy, memory usage, and processing time** without storing all data in memory.

---

## 2. 데이터셋 (Dataset)

### MovieLens 1M Dataset

- 총 레코드 수(Total Records): **1,000,209**
- 사용 파일(File Used): **ratings.dat**
- 데이터 형태(Data Type): 사용자-영화 평점 이벤트 스트림

### 컬럼 설명 (Columns)

| Column | Description |
|--------|-------------|
| UserID | 사용자 ID |
| MovieID | 영화 ID |
| Rating | 영화 평점 |
| Timestamp | 이벤트 발생 시간 |

### 데이터셋 다운로드

MovieLens 1M 공식 데이터셋:

:contentReference[oaicite:0]{index=0}

실행 전 `ratings.dat` 파일을 다운로드 후 업로드해야 합니다.

Before execution, download the dataset and upload `ratings.dat`.

---

## 3. 구현 알고리즘 (Implemented Algorithms)

### 1) Bloom Filter

**목적(Purpose)**  
원소 포함 여부를 근사적으로 판별

Approximate membership query.

**특징**
- 빠른 탐색 속도
- 적은 메모리 사용
- False Positive 발생 가능
- False Negative 없음

---

### 2) Count-Min Sketch

**목적(Purpose)**  
항목별 등장 빈도 근사 추정

Approximate frequency estimation.

**특징**
- 적은 메모리 사용
- 빠른 빈도 추정
- Hash collision 기반 오차 발생 가능

---

## 4. 실험 내용 (Experimental Analysis)

다음 항목을 비교 분석하였다.

### Accuracy Comparison
- Bloom Filter → False Positive Rate
- Count-Min Sketch → Relative Error

### Memory Usage Comparison
- 자료구조 크기 비교
- 파라미터 변화에 따른 메모리 변화 분석

### Processing Time Comparison
- 전체 처리 시간 비교
- 스트림 처리 효율성 분석

### Parameter Sensitivity Analysis
- Bloom Filter: bit array size, hash function 수
- Count-Min Sketch: width, depth

---

## 5. 실험 환경 (Environment)

- Python 3.x
- Google Colab
- pandas
- numpy
- matplotlib
- hashlib

---

## 6. 최종 결론 (Conclusion)

본 프로젝트에서는 스트리밍 환경에서 정확도와 메모리 사이의 Trade-off 관계를 분석하였다.

실험 결과:

- 메모리 증가 → 정확도 향상
- 파라미터 증가 → 항상 성능 향상 X
- 목적에 따라 적합한 알고리즘이 달라짐

실제 서비스 로그 분석 환경에서는 **Bloom Filter + Count-Min Sketch 조합이 가장 실용적**이라고 판단하였다.
