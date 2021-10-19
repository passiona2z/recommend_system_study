v21.10.19

## 최근접이웃 협업 필터링 방식
##### 키워드 : 행동 이력, (사용자-아이템)행렬, 예측 평가


#### [개념]

**사용자 A**의 **축척된 행동이력**(평점 정보, 구매 정보)을 기반으로,
</br>사용자 A가 **아직 평가하지 않은 아이템의 평가를 예측**하여 추천 

  - (중요) **아이템의 콘텐츠(속성)과는 무관하게** 사용자의 행동 이력만을 토대로 추천 

- 사용자 기반 : "당신과 비슷한 고객들이 다음 상품도 구매했습니다"
  - 특정 사용자와 타 사용자 간의 **행동 이력(등록 평점 등)을 기반으로 유사도를 측정**
  - **유사도가 높은 사용자를 추출**해 **그들이 선호하는 ITEM**을 추천
  - (예) '딸기', '수박'를 좋아하는 사용자 A <> '딸기', '수박', '귤'를 좋아하는 사용자 B
          (사용자A, B는 취향이 유사하다는 전제) 사용자A 에게 사용자 B가 좋아하는 '귤'을 추천 

- 아이템 기반 : "이 상품을 선택한 다른 고객들은 다음 상품도 구매했습니다"
  - 사용자들의 **행동 이력(등록 평점 등) 분포를 기반으로 ITEM간의 유사도를 측정**
  - 특정 ITEM을 선호하는(좋아하는) 사용자에게 **유사도가 높은 ITEM을 추천**
  - (예) 포도는 사용자 A, B, C가 선호, 수박은 사용자 A, B가 선호
         (포도와 수박은 선호 기준으로 유사하다는 전제) 사용자C에게 '수박'을 추천
        
<img src="https://user-images.githubusercontent.com/75558808/137833209-c3754019-090a-4b62-bd31-94d40a3194cf.png"  width="500" height="300"/>




#### [코드 구현 프로세스]

1. **(사용자 - 아이템) 행렬 또는 (아이템 - 사용자) 행렬** 
   - 두 행렬을 서로 전환할 경우 전치행렬 사용
2. 코사인 유사도 등으로 **유사도 산출**
3. 사용자가 구매하지 않은 아이템에 대한 **예측 평가 계산**
   - 유사도 등을 반영
4. **예측 평가가 높은 순**으로 아이템 추천