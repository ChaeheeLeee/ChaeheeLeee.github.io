---
title: "[파이썬머신러닝완벽가이드] 10장. 시각화"
description: KHUDA과제 1
author: ChaeheeLeee
date: 2026-01-20 03:33:00 +0900
categories: [KHUDA, 파이썬머신러닝완벽가이드]
tags: [KHUDA, 파이썬머신러닝완벽가이드]
pin: true
math: true
mermaid: true

---
#10-1 시각화를 시작하며 - 맷플롯립과 시본 개요
{: .mt-4 .mb-0 }

맷플롯립: 파이썬 시각화의 표준 라이브러리, 하지만 코딩에 불푠함이 있고 디자인이 투박함

시본: 맷플롯립보다 쉬운 구현, 수려한 시각화, 판다스와 연동이 쉬움

#10-2 맷플롯립(Matplotlib)
{: .mt-4 .mb-0 }

pyplt의 중요 요소: Figure(객체 그림을 그리는 캔버스), Axes(실제 그래프가 그려지는 영역) (+Axis(축))

plt.figure(): figure의 크기를 조절

plt.plot(): 선 그래프 생성

plt.show(): 그래프 출력

여러 개의 plot을 가지는 subplot들을 생성하기:

plt.subplots() -> 여러개의 subplot을 생성하는 데 활용

plt.subplots(nrows=1, ncols=2, figsize=(6,3)) -> Figure와 두 개의 Axes 객체를 반환

이때 반환되는 Axes 객체는 (ax1, ax2)와 같이 튜플 형태로 반환


-축의 여러가지 설정하기

plt.xlabel() / plt.ylabel(): X, Y축 이름 설정

xticks() / yticks(): 눈금값 회전

legend(): 범례를 Axes 상에 표시

#10-3 시본(Seaborn)
{: .mt-4 .mb-0 }

X축과 Y축으로 구성된 이차원 축에서 데이터를 시각화해준다. -> 2개의 변수에 대한 정보 표출

히스토그램: sns.histplot() -> 연속으로 이어진 막대그래프 형태의 히스토그램 생성

kde=True: 히스토그램의 연속 확률분포 곡선까지 함께 시각화

카운트 플롯: sns.countplot() -> 이산형 값의 건수를 막대그래프로 시각화

바 플롯: sns.barplot() -> 2차원 축 기반 시각화에 주로 사용

박스 플롯: sns.boxplot() -> 분위수 기반, 연속형 값에 적용해야 좋음

바이올린 플롯: sns.violinplot() -> 연속 확률 분포 곡선과 박스 플롯을 함께 시각화, 연속형 값에 적용해야 좋음

산점도, 스캐터 플롯: sns.scatterplot() -> 좌표상에 점 표시, 변수간의 관계를 나타냄

상관 히트맵: sns.heatmap() -> 다수의 속성들 간의 상관계수를 색상으로 시각화

True -> 상관계숫값 표시

cmap -> 히트맵의 색상 변경