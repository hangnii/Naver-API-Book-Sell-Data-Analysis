# Naver API Book Sell Data Analysis
- 인기 프로그래밍 언어 데이터를 수집하여, 네이버 책 검색 API를 활용해 언어별 도서 출판량 및 양상을 비교 분석한 EDA 프로젝트

## 1. TIOBE INDEX 페이지 크롤링
![image](https://user-images.githubusercontent.com/92846399/150674878-7fea9877-2c1f-45a5-9588-ba796d7a2f83.png)
- 상위 1~9위의 언어에 R까지 합쳐 총 10개의 언어를 대상으로 분석 범위를 정함.
  - 이는 2020년도 순위 기준 1~10위와 동일.

## 2. 각 언어별 출판도서 데이터 수집

![image](https://user-images.githubusercontent.com/92846399/150674905-9551b15a-5423-4764-b9f3-37b92310c0c6.png)

### 1) 네이버 검색 API를 사용하여 도서 검색 
- '총 검색 결과 수'와 언어별로 출판된 책의 '제목', '출판사', '출판일', '가격', 'ISBN', '책 링크' 등의 데이터를 수집.
- 'C'나 'R'같은 한 글자 언어의 경우, 정확한 검색이 어려워 ‘상세 검색’ 방법을 이용.
  - 상세검색을 위한 조건:
    - 책 제목(d_titl)
    - 카테고리(d_catg): IT 전문서(280020)

- 검색 url을 만들어주는 함수를 검색량 변화의 확인을 위해 세 가지 형태로 생성.
  - 1) 기본 검색 url
  - 2) '책 제목' 조건 사용
  - 3) '책 제목'과 '카테고리' 조건 사용
  - 전체 검색 건수를 대략적으로 확인해보니, 검색방법마다 검색결과 수의 편차가 큼.
  - 네이버 API의 검색 제한량이 **1000개**라는 점을 감안하여 제목과 카테고리를 사용하는 세 번째 함수 선택.

- 1차 중복제거
  - 동일 언어 내에서 중복되는 ISBN 제거
- 데이터 형 변환
  - 가격(=> float)
  - 출판일(=> datetime)



<br/>

### 2) 중복데이터 삭제
- 동일한 언어이지만 다른 검색어로 검색된 결과 하나로 통일
  -  자바스크립트/JavaScript, 파이썬/Python 등
- 'Java'와 'JavaScript' 차집합으로 교차검증
  - JavaScript에만 데이터를 남기고 제거.
![image](https://user-images.githubusercontent.com/92846399/150676098-7ecb86e8-f68f-4beb-88ac-043e99d3792d.png)

## 3. 주제별 시각화 및 분석

### 1. 언어별 출판물 순위
- C, Java, C++, Python, VB, SQL, JavaScript, C#, R, PHP 순.
<br/>

- 2021년 TIOBE INDEX와 비교
![image](https://user-images.githubusercontent.com/92846399/150676115-703f7065-148f-47f0-9c2d-ae0a226d4972.png)
- 2020년 TIOBE INDEX와 비교
![image](https://user-images.githubusercontent.com/92846399/150676125-6550064a-e538-48d3-ba95-01bc4d1aeb44.png)

### 2. 국내 IT서적 출판사별 출판량 순위
- 국내 출판 서적으로 범위를 한정하기 위해 ISBN의 국가식별코드를 사용하여 데이터를 필터링
  - ![image](https://user-images.githubusercontent.com/92846399/150676300-79de4241-7b0f-4f10-91a1-bce8f68358fe.png)

-  IT서적 출판사별 출판건수를 나타낸 그래프
  - ![image](https://user-images.githubusercontent.com/92846399/150676577-aef4104c-6e36-419c-b4dd-b24a86cfdfe9.png)

- 출판사 고유값 : 552개
  - 5권 이하: 392개
    - 1권 출판: 195개 
  - 100권 이상: 12개
    - 200 ~ 300권 : 1개 (영진닷컴)
    - 300 ~ 400권 : 2개 (에이콘출판, 정보문화사)
    - 400권 이상 : 1개 (한빛미디어)
![image](https://user-images.githubusercontent.com/92846399/150676634-4a32cb91-5113-471b-b42a-e92582bb2993.png)
- 누적그래프
- ![image](https://user-images.githubusercontent.com/92846399/150676694-45afea5a-ab1a-4be6-b177-0d00bd757dd8.png)
  - 언뜻 보면 **파이썬, C, Java** 삼대장이 많아 보임.
  - 자세히보면 출판사별로 많이 출판하는 프로그래밍 언어가 다양하게 분포.
  - 여러가지 언어를 골고루 출판하는 출판사도 많음.





### 3. 출판연도별 비교
![image](https://user-images.githubusercontent.com/92846399/150676756-32bd5654-1384-4b51-8033-e6253d6c6c84.png)
- 최근 5년간 언어별/연도별 출판량
![image](https://user-images.githubusercontent.com/92846399/150676799-bf8fdc7c-0e0e-492f-9306-6b83d7090923.png)
- 연도별 출판사별 출판 언어 순위
  - 17-19년에 출판된 출판사별, 언어별 도서량
  - ![image](https://user-images.githubusercontent.com/92846399/150677207-b54a9144-a0c9-4778-9d9b-807acffbbf38.png)

  - 최근 2년(20-21)간 출판된 출판사별, 언어별 도서량
  ![image](https://user-images.githubusercontent.com/92846399/150675005-2f63490b-2ea3-456c-b242-03322bdbbb5b.png)
  - 파이썬(파란색)이 차지하는 비중이 확 늘어난 것을 체감할 수 있음.
<br/>

  - ![image](https://user-images.githubusercontent.com/92846399/150677151-61f39816-fd2f-4eae-87b9-99178b7b0beb.png)

<br/>

- 언어별/연도별 출판량
![image](https://user-images.githubusercontent.com/92846399/150676815-97d78072-2448-45c3-b20e-f21a173abac2.png)
  - 초창기  C,  C++  점령
  - 1999년 비주얼베이직 정점
  - 2002년 자바 정점
  - 2019년 파이썬 정점(역대급 수치)

![image](https://user-images.githubusercontent.com/92846399/150676880-48335f72-4d8b-4dff-9cf2-e91abdb7e917.png)

  - 파이썬이 2019년에 정점을 찍고 다시 감소한 이유는, 언어의 인기나 수요가 줄어서라기 보다는 **코로나19**로 인한 '전체 출판시장의 축소' 때문일 것.



### 5. 책 가격과 페이지 수의 상관관계
#### 1. Pair Plot
![image](https://user-images.githubusercontent.com/92846399/150677385-86137870-d19a-4237-80bc-676b38367bc5.png)

#### 2. LM Plot (corr=0.6044)
![image](https://user-images.githubusercontent.com/92846399/150677346-976564f5-d7f3-46dc-afde-7bc3880f0890.png)

- pairplot,lmplot,상관계수를 확인해 본 결과, 책 가격과 페이지 간 상관관계가 유의미하다고 볼 수 있다.


#### 3. Scatter Plot
![image](https://user-images.githubusercontent.com/92846399/150677411-419fa1d7-aaa5-4fdc-88df-2ec03caf0292.png)

- 특이점
  - R은 가격대는 최상위권이나, 페이지 수는 최하위권
  - Python 역시 가격대는 상위권이나, 페이지 수는 최하위권
  - Visual Basic은 반대로 가격대는 가장 저렴한데 페이지 수는 많은 편
  - 앞선 그래프들과 달리 회귀선이 하향세

<br/>
#### 4. Box Plot

- ![image](https://user-images.githubusercontent.com/92846399/150677476-5f4e48ad-40bc-4885-b28e-2493cc2fdd24.png)
  - 가격, 페이지 수 모두 **한국 > 해외**
<br/>

- ![image](https://user-images.githubusercontent.com/92846399/150675091-a1344d59-9ee0-49b9-aa14-cdf00045b6a0.png)
    - 8만원을 넘는 책 5권
      - SQL / 16만원 / 1000p
      - (1998) MS사 -> 삼각형
      - C/약12만원/1948p - (2013) 전 4권 세트
      - Java / 약11만원 / 2456p - (2015) 전 3권 세트
      - 파이썬/약10만원/245p - (2021) 드론 포함 가격
      - C/약9만원/1996p
      - (2014) 전 2권 세트

- ![image](https://user-images.githubusercontent.com/92846399/150675075-a51a0d28-6687-4108-ae4b-919ac31ea317.png)

- hue=출판국가
- ![image](https://user-images.githubusercontent.com/92846399/150675060-8ffbb5b6-c481-4eb9-81f9-50b6edcfabb9.png)

  - 파이썬, 자바, 자바스크립트는 해외 vs 국내 가격대가 크지 않은데 반해 C, C++, PHP, R은 꽤 차이가 난다.
  - SQL은 해외서적의 가격 분포가 넓고, 페이지 수는 가장 낮은 편이다.
  - 파이썬의 경우 해외 서적이 국내 서적보다 페이지 수가 더 많은데, 가격은 더 저렴하다.
  - 페이지 수 박스 길이(분포)를 보면, 파이썬과 R은 좁고, C#, 비주얼베이직은 넓다.

#### 결론:
종합적으로 보았을 때,
프로그래밍 언어 책의 가격을 결정하는 요소로
책의 페이지 수 뿐만 아니라
수요(인기도), 기존에 형성된 가격대, 보급 및 상용화된 기간, 각 프로그램 언어를 사용하는 주 연령대의 차이 등
다양한 변수들이 영향을 미칠 수 있을 것이라 예측할 수 있음.
