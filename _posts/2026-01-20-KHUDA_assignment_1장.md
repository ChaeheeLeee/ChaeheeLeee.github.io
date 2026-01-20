---
title: "[파이썬머신러닝완벽가이드] 1장. 파이썬 기반의 머신러닝과 생태계 이해"
description: KHUDA과제 1
author: ChaeheeLeee
date: 2026-01-20 03:33:00 +0900
categories: [KHUDA, 파이썬머신러닝완벽가이드]
tags: [KHUDA, 파이썬머신러닝완벽가이드]
pin: true
math: true
mermaid: true

---
# 1-1 머신러닝의 개념
{: .mt-4 .mb-0 }

머신러닝: 지도학습(분류, 회귀)/비지도학습

단점: 데이터에 매우 의존적이다.

파이썬과 R: 개발자들에게는 파이썬을 추천


# 1-2 파이썬 머신러닝 생태계를 구성하는 주요 패키지
{: .mt-4 .mb-0 }
머신러닝 패키지: 사이킷런

행렬/선형대수/통계 패키지: 넘파이 > 행렬 기반의 데이터 처리

데이터 핸들링: 판다스 > 2차원 데이터 처리에 특화, 넘파이보다 편리하다.

시각화: 맷플롯립 > 하지만 투박하다 / 시본 > 맷플롯립 기반, 효율이 더 좋다.

아이파이썬 툴: 대화형 툴, 특정 코드 영역별로 개별 수행을 지원 > 주피터 노트북


# 1-3 넘파이
{: .mt-4 .mb-0 }

넘파이: 선형대수 기반의 고성능 배열 연산 패키지, 루프 없이 대량 데이터 연산 가능하다.

ndarray: 넘파이의 기반 데이터 타입. 같은 데이터 타입만 담을 수 있다. (int와 float 혼용 시 큰 타입으로 변환)

astype: ndarray 내 데이터 값의 타입 변경

arange(): range처럼 연속된 값 생성

zeros()/ones(): 0 또는 1로 채운 배열 생성

reshape: 배열의 차원과 크기를 변경, 인자에 -1을 쓰면 나머지 차원에 맞춰 자동 변환된다.


[인덱싱]

array[1] -> 2번째 위치의 데이터 값(인덱스 -1은 맨 뒤의 데이터값)

axis 0 -> 로우 방향의 축

axis 1 -> 칼럼 방향의 축

슬라이싱:  : 기호로 연속된 인덱스상의 ndarray를 추출

array1 = np.array(start=1, stop=0)

array1[:3] -> 3번째 위치의 값까지. [1 2 3]

array1[3:] -> 4번째부터 그 뒤의 값까지. [4 5 6 7 8 9]

array1[:] -> 전체 출력. [1 2 3 4 5 6 7 8 9]

-2차원 슬라이싱

array1d = np.array(start=1, stop=10)

array2d = array1d.reshape(3, 3)

array2d[0:2, 0,2] ->

[[1 2]

[4 5]]

array2d[1:3, :] ->

[[4 5 6]

[7 8 9]]

2차원 ndarray에서 뒤에 오는 인덱스를 없애면 1차원 ndarray를 반환.


팬시 인덱싱: 리스트나 ndarray로 인덱스 집합을 지정해 해당 위치의 데이터를 추출 

array2d[[0, 1], 2] -> [3, 6]

array2d[[0, 1], 0:2] -> [[1, 2], [4, 5]]

불린 인덱싱: 조건 필터링과 검색을 동시에 수행

array1d = np.arange(start=1, stop=10)

array1d > 5 -> [False, False, ... True, True]

array1d[array1d > 5] -> True에 해당하는 인덱스의 데이터만 반환. [6 7 8 9] 

행렬 정렬

np.sort(array) -> 원본 미변경, 정렬된 형태 반환 

array.sort() -> 원본 자체를 정렬해서 변환, 반환 값은 None 

np.argsort(array) -> 정렬된 행렬의 원본 행렬 인덱스를 반환

내림차순 정렬: np.sort(array)[::-1], np.argsort(array)[::-1] 


선형대수 연산

행렬 내적(곱): np.dot(A, B) -> 왼쪽 행렬의 로우와 오른쪽 행렬의 칼럼 원소들의 곱의 합 

전치 행렬: np.transpose(A) -> 행과 열의 위치를 교환


# 1-4 데이터 핸들링-판다스
{: .mt-4 .mb-0 }

DataFrame: 행과 열로 이뤄진 2차원 데이터를 담는 구조체 (Index + Series들로 구성) 

pd.read_csv('파일명'): CSV 파일을 DataFrame으로 로딩 

shape: 행과 열의 크기를 튜플로 반환 -> (891, 12) 

info(): 총 데이터 건수, 데이터 타입, Null 건수 확인 

describe(): 숫자형 칼럼의 개략적인 분포도(평균, std, min, max 등) 확인 

value_counts(): 특정 칼럼의 데이터값 건수 반환 (데이터 분포 확인에 유용) 

dropna=False 인자 사용 시 Null 값 포함하여 계산 

변환 (DataFrame <-> 넘파이, 리스트, 딕셔너리)

df.values: DataFrame을 넘파이 ndarray로 변환

df.values.tolist(): 리스트로 변환 

df.to_dict('list'): 딕셔너리로 변환 

df['새칼럼명'] = 0: 모든 데이터에 0 할당

df['기존칼럼명'] = df['기존칼럼명'] + 100: 기존 칼럼 값 일괄 업데이트 

데이터 삭제: drop() 

axis=1: 칼럼(열) 삭제 

axis=0: 로우(행) 삭제 

inplace=True: 원본 DataFrame 자체를 변경 (반환값 None) 

예: titanic_df.drop('Age_0', axis=1, inplace=True) 

-Index 객체

식별용으로만 사용되며 연산에서 제외됨 

reset_index(): 인덱스를 연속 숫자형으로 새로 할당, 기존 인덱스는 'index' 칼럼으로 추가됨 

-데이터 셀렉션 및 필터링

[] 연산자: 칼럼명 지정 또는 불린 인덱싱 용도로만 사용 권장 

df['Col1'] (O), df[0] (X, 오류 발생) 

df[0:2] 처럼 슬라이싱은 가능하나 비추천 

iloc[] (위치 기반): 행/열 위치를 0부터 시작하는 정수로 지정 

df.iloc[0, 0] -> 첫 번째 행, 첫 번째 열 데이터 

df.iloc[:, -1] -> 맨 마지막 칼럼 데이터 (타깃 값 추출 시 사용) 

loc[] (명칭 기반): 인덱스 값과 칼럼명으로 지정 

df.loc['index_name', 'Col_name']

주의: 슬라이싱 시 Start:End에서 End값까지 포함

불린 인덱싱: [], loc[]에서 공통 지원

df[df['Age'] > 60] 

복합 조건: & (and), | (or), ~ (not) -> df[(cond1) & (cond2)] 


-Aggregation 함수 적용

sort_values(by=['칼럼명']): 해당 칼럼 기준으로 정렬 (ascending=False는 내림차순) 

Aggregation: min(), max(), sum(), count() 등 

df.count(): Null 값을 제외한 데이터 건수 반환 

groupby(): by 인자에 칼럼 입력 시 해당 칼럼 기준으로 그룹화 

df.groupby('Pclass').count() 

agg(): 여러 개의 집계 함수 적용 시 사용 -> df.groupby('Pclass')['Age'].agg([max, min]) 


-결손 데이터 처리하기

isna(): NaN 여부 확인 (True/False) -> df.isna().sum()으로 결손 데이터 개수 확인 가능 

fillna(): 결손 데이터를 다른 값으로 대체 

df['Age'].fillna(df['Age'].mean(), inplace=True): 평균값으로 대체 

-apply lambda 식

복잡한 데이터 가공 시 함수형 프로그래밍처럼 적용 

lambda x: (반환값) if (조건) else (반환값) 형태 

df['Name_len'] = df['Name'].apply(lambda x: len(x))