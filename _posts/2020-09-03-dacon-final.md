---
title: "COVID19 발발 이후 수도권 지하철 빅데이터 분석을 통한 이용자 유형별 이동 패턴 분석 "
date: 2020-09-03 08:26:28 +0900
categories: dataviz
---


# COVID19 발발 이후 수도권 지하철 빅데이터 분석을 통한 이용자 유형별 이동 패턴 분석 
***

<div style="background-color:rgba(8, 14, 51, 1); text-align:center; vertical-align: middle; padding:1px 0;">
    <h2><center style = "color: white"> 개요 </center></h2>
</div>

## 들어가며
<b>지하철은 도시의 동맥입니다.</b> COVID19의 확산 이후 사회적 거리두기 캠페인, 원격 수업, 영업 규제 등이 국민들의 이동을 제한하여 작년 대비 이용량이 줄었지만 지하철은 여전대한민국의 국가경제 활동에 지대한 기여를 하고 있습니다. 

하지만 지하철의 3밀 조건 (밀집, 밀폐, 밀접)은 COVID19과 같은 전염병 확산에 큰 영향을 미치기도 합니다. 지하철 이용이 공공 보건에 끼칠 수 있는 잠재적 위험을 분석하기 위해 지하철 이용 관련 빅데이터를 분석하였습니다. 인구가 집중되어 있고 현재까지 적지 않은 클러스터가 발생한 서울 지역을 종합적으로 이해하기 위해서는 수도권 지구의 위성 도시들에 대한 이해가 필요합니다. 따라서 저희는 수도권 전철에 대한 포괄적인 분석을 위해 “한국교통안전공단 교통카드 데이터”를 사용하여 COVID19 확산 전후의 지하철 이용 패턴을 분석하였습니다. 특히 특이 현상을 보이는 두 개 유형, 노령 인구와 청소년 인구를 중점으로 분석을 진행하였습니다.

한국교통안전공단 데이터를 GIS정보를 활용해 시각화하고, 이용자 유형별로 나누어 패턴을 살펴보면서 노령 인구와 청소년 인구의 특수성을 고려한 COVID19에 대한 교통 차원의 대응 방안과 수도권 교통 문제에 대한 전반적인 제언을 마련하였습니다.


## 목차
<ul>
<li> 0. 데이터 전처리</li>
<li>1. COVID19가 지하철 이용량에 미친 영향
<ul>
<li>Q1-1. 코로나 바이러스는 지하철 이용량에 어떤 영향을 미쳤을까?</li>
<li>Q1-2. 코로나 바이러스에 대응하는 정부 정책은 지하철 이용량에 어떤 영향을 미쳤을까?</li>
<li>Q1-3. 각 지하철 역들의 이용량은 어떻게 변화하였을까?</li>
</ul>
</li>
<li>2. 이용유형별 세분화를 통한 패턴 분석
<ul>
<li>Q2-1. 각 유형별 지하철 이용자들은 “사회적 거리두기 캠페인"에 얼만큼 영향을 받았을까?</li>
<li>Q2-2. 경로/청소년 이용객의 증감율은 어떤 특성을 가지고 있을까?
</li>
</ul>
</li>
<li>3. 경로 (65세 이상 인구)의 지하철 이용유형 패턴 분석
<ul>
<li>Q3-1. COVID19가 연령층 별로 미치는 영향은 어떤 차이가 있을까?
<li>Q3-2. “경로우대 교통카드"를 사용하는 65세 이상 인구는 어떤 사회 활동에 참여할까?
</li>
<li>Q3-3. 왜 65세 이상 인구의 지하철 이용량이 크게 줄지 않았을까?</li>
</ul>
</li>
<li>4. 청소년 (13-18세 이상 인구)의 지하철 이용유형 패턴 분석
<ul>
<li>Q4-1. 청소년이 이용하는 역이 주중과 주말 어떻게 다를까?</li>
<li>Q4-2. 주중 대비 주말 청소년의 지하철 이용량 증가가 시사하는바는 무엇일까?
</li>
</ul>
</li>
<li>5. 제언: 향후 정책에 반영할 점들
<ul>
<li>노령 인구 지하철 이용 패턴의 특수성을 고려한 해결책: 수도권 외곽 지역에서 수도권 중심부를 잇는 교통편 구축</li>
<li>청소년 인구 지하철 이용 패턴의 특수성을 고려한 해결책: 다른 역으로 흩어질 수 있는 좋은 환경 만들기</li>
<li>마치며
</li>
</ul>
</li>
</ul>


## 활용 데이터
<b> [DACON 제공 데이터]</b>

<ul>
<li>한국교통안전공단 교통카드 데이터 
<ul>
<li>DM_STTNBY_USECNT_T (정류장별 이용량)</li>
<li>DD_AREA (지역코드) </li>
<li>DM_STTN_T (정류장)</li>
</ul>
</li>
<li> DS4C팀 COVID-19 데이터
<ul>
<li>Policy</li>
</ul>
</li>
</ul>


<b>[외부 데이터 및 자료]</b>
- [Naver Map API][1]
- [서울시 노인 사회활동 참가 통계][2]
- [Young Joon Park, et al., "Contact Tracing during Coronavirus Disease Outbreak, South Korea, 2020," Emerging Infectious Diseases (October 2020)][3]
- [청소년상담 이슈페이퍼][4]
- [Jewel Park, "Changes in Subway Ridership in Response to COVID-19 in Seoul, South Korea: Implications for Social Distancing," Cureus, April 14, 2020][5]

[1]: https://www.ncloud.com/product/applicationService/maps
[2]: https://data.seoul.go.kr/dataList/47/S/2/datasetView.do#
[3]: https://wwwnc.cdc.gov/eid/article/26/10/20-1315_article
[4]: https://www.kyci.or.kr/fileup/issuepaper/IssuePaper_202002.pdf
[5]: https://www.cureus.com/articles/30376-changes-in-subway-ridership-in-response-to-covid-19-in-seoul-south-korea-implications-for-social-distancing 

## 방법
- Python pandas, selenium 등을 활용한 데이터 전처리
- Tableau 및 matplotlib를 활용한 line graph, bump chart, map visualization 제작

## 결과
- 노령 인구의 경우 지하철 의존도가 높은 것으로 드러남. 특히 수도권 외곽 지역인 인천 지역 노령 인구의 지하철 의존도가 높은 것으로 드러남.
- 청소년 인구의 경우 사회적 거리두기 및 개학 연기령 실시 이후엔 큰 감소를 보이다가, 시간이 지날수록 이용률에 있어 큰 회복세를 보임. 특히 주말의 경우에는 보복 소비(revenge spending) 의 일환으로 다른 연령대에 비해 주중 대비 큰 증가세를 보임.
- COVID19과 같은 전염병 확산 대응 및 포스트 코로나 시대를 준비하기 위해 천편일률적인 정책이 아닌 연령대별/지역별 특성을 고려한 다각화된 접근 방법이 필요하다는 것을 확인.

## 제언
- 지하철 의존도가 높은 수도권 외곽 지역 (특히 인천)의 노령 인구를 위하여 수도권 외곽 지역에서 수도권 중심부를 잇는 교통편 구축하기.
- 주말 인구 밀집 현상을 보이는 청소년 인구를 위하여 하나의 지하철 역에서 다른 역으로 자연스럽게 분산될 수 있는 환경 조성하기.
- 교통 관련 데이터를 일반 시민들도 활용할 수 있는 환경 및 툴 마련하기. 

## 한계
- 연구 대상 지역의 절대 인구수 증감이 2019년과 2020년 지하철 증감률에 영향을 주었을 수 있음.
- 지하철뿐만 아니라 버스를 포함한 전반적인 대중교통 변화에 대한 분석이 추가로 필요함. 

***
<div style="background-color:rgba(8, 14, 51, 1); text-align:center; vertical-align: middle; padding:1px 0;">
    <h2><center style = "color: white"> 데이터 전처리</center></h2>
</div>

### <u>Step 0. Setup</u>
### 1. 필요한 라이브러리  Import


```python
import urllib.request
import requests

from csv import reader
import numpy as np
import pandas as pd
from datetime import datetime
import warnings; warnings.simplefilter('ignore')

# 데이터 전처리 Step 5 Web scraping용
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.common.exceptions import TimeoutException
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By

# 시각화 라이브러리 
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
import matplotlib.font_manager as fm
font_path = 'font/NanumBarunGothic.ttf'
fontprop = fm.FontProperties(fname=font_path, size=18)
from IPython.core.display import Image, display
from IPython.display import IFrame, HTML

from geopy.distance import geodesic
```

### 2. 함수 정의하기


```python
def findStreetAddress(df):
    """
    Step 5에 사용: dataframe이 주어졌을 때 네이버 지도 서비스를 사용하여 각 정류장 명칭에 해당되는 도로명 주소를 찾기 
    Input: dataframe
    Output: dataframe (Input된 dataframe에 "Sel 검색명칭", "Sel 검색결과", "Sel 카테고리", "Sel 주소"가 추가됨)
    """
    driver = webdriver.Chrome(ChromeDriverManager().install())

    query_list = [] # 검색 명칭을 저장 
    title_list = [] # 제일 위에 나온 검색 결과의 타이틀을 저장
    category_list = [] # 제일 위에 나온 검색 결과의 카테고리를 저장
    address_list = [] # 제일 위에 나온 검색 결과의 주소를 저장 
    for index, row in df.drop_duplicates(["정류장 명칭", "정류장 ID"]).iterrows():
        split = row["정류장 명칭"].split("[") 
        current_station = split[0].replace(" ","역 ") + split[1].replace("]", "")
        query_list.append(current_station)

        # https://m.map.naver.com/search2/search.nhn?query= 끝에 검색하고 싶은 장소를 정하면 해당 장소가 네이버 지도를 통해 검색이 됩니다.
        driver.get('https://m.map.naver.com/search2/search.nhn?query='+current_station) # 웹페이지 열기  
        timeout = 2
        try:
            element_present = EC.presence_of_element_located((By.ID, 'main'))
            WebDriverWait(driver, timeout).until(element_present) # 페이지가 열릴 때까지 timeout (2초) 대기
        except TimeoutException:
            status = 1 

        search_title_text = driver.find_elements_by_css_selector('.item_tit._title') # 클래스가 .item_tit._title인 element 찾기
        try: 
            search_title_text[0].find_element_by_tag_name('strong').get_attribute('innerHTML')
        except IndexError: # 검색 결과가 없거나 홈페이지 로드에 에러가 있었을 경우
            title_list.append("") # ""을 placeholder로서 추가
        else: 
            title_list.append(search_title_text[0].find_element_by_tag_name('strong').get_attribute('innerHTML'))

        search_text_category = driver.find_elements_by_css_selector(".item_tit._title") # 클래스가 .item_tit._title인 element 찾기
        try: 
            search_text_category[0].find_element_by_tag_name('em').get_attribute('innerHTML')
        except IndexError: # 검색 결과가 없거나 홈페이지 로드에 에러가 있었을 경우
            category_list.append("") # ""을 placeholder로서 추가
        else: 
            category_list.append(search_text_category[0].find_element_by_tag_name('em').get_attribute('innerHTML'))

        search_text_address = driver.find_elements_by_css_selector(".item_address._btnAddress") # 클래스가 .item_address._btnAddress인 element 찾기
        try: 
            search_text_address[0].get_attribute('innerHTML')
        except IndexError: # 검색 결과가 없거나 홈페이지 로드에 에러가 있었을 경우
            address_list.append("") # ""을 placeholder로서 추가
        else: 
            address_list.append(search_text_address[0].get_attribute('innerHTML').replace('<i class="btn_tgg_address">주소보기</i>                               ',''))

    df["Sel 검색명칭"] = query_list
    df["Sel 검색결과"] = title_list
    df["Sel 카테고리"] = category_list
    df["Sel 주소"] = address_list
    return df
```


```python
def findCoord(df):
    """
    Step 6에 사용: dataframe이 주어졌을 때 Naver Map API를 사용하여 각 도로명 주소에 해당되는 위도, 경도 찾기  
    Input: dataframe
    Output: dataframe (Input된 dataframe에 "long", "lat"이 추가됨)
    """
    df['long'], df['lat'] = "", ""
    for x in range(len(df)):
        # naver map api에 request 보내기 
        url = "https://naveropenapi.apigw.ntruss.com/map-geocode/v2/geocode?query=" + urllib.parse.quote(df['Sel 주소'][x])
        request = urllib.request.Request(url)
        request.add_header("X-NCP-APIGW-API-KEY-ID", client_id)
        request.add_header("X-NCP-APIGW-API-KEY", client_secret)
        response = urllib.request.urlopen(request)
        
        rescode = response.getcode()
        if(rescode == 200):
            response_body = response.read()
            mydic = eval(response_body.decode('utf-8'))
        else:
            print("Error Code:" + rescode)
            
        dict_ = {"long":"x", "lat":"y"}
        for key in dict_:            
            try: 
                df[key][x] = mydic['addresses'][0][dict_[key]]
            except IndexError: # request의 response에 문제가 있는 경우
                df[key][x] = 999999 # 999999를 placeholder로서 추가
            else:
                df[key][x] = mydic['addresses'][0][dict_[key]]   
    return df
```

### <u>Step 1. Data Schema 제작: [링크](https://dbdiagram.io/d/5f3bb327cf48a141ff554703)</u>


```python
display(Image('img/schema.png', unconfined=False, width = 600))
```


![png](/assets/images/dacon-final_7_0.png)


'한국교통안전공단 교통카드 데이터' 같은 경우 용량도 클 뿐만 아니라 각각 다른 역할을 하고 있는 여러 테이블이 연결되어있는 구조였기 때문에 제공된 정의서만으로 분석을 진행하기에는 불편함이 있었습니다. 그러한 불편함을 극복하고 테이블간의 손쉬운 관계 파악을 위해 제공된 정의서에 기반하여 간단한 Data Schema를 제작하였습니다. DM_STTNBY_USECNT_T (정류장별 이용량) 테이블을 주로 사용할 예정이었기에 DM_STTNBY_USECNT_T과 관련된 테이블들만 입력하였습니다.
### <u> Step 2. DM_STTNBY_USECNT_T (정류장별 이용량) 테이블 필터링</u>
DM_STTNBY_USECNT_T 테이블를 통해서 수도권뿐만 아니라 전국의 정류장별, 시간대별 승하차 인원을 확인할 수 있습니다. 

이번 분석에는 수도권에 집중을 한만큼 DD_AREA (지역코드) 테이블을 활용하여 시도 코드 11은 서울특별시, 28은 인천광역시, 41은 경기도라는 것을 확인하였습니다. 


```python
DD_AREA = pd.read_csv("data/card/CARD_0001/DD_AREA.dat", sep='|', header=None)
DD_AREA.columns = ["지역 구분","시도 코드","시군구 코드","이용 지역 코드","시도 명","시군구 명","읍면동 명"]
DD_AREA[DD_AREA["시도 명"].str.contains("서울|인천|경기")].drop_duplicates(["시도 코드", "시도 명"])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>지역 구분</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>시도 명</th>
      <th>시군구 명</th>
      <th>읍면동 명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>11</td>
      <td>11000</td>
      <td>1100000000</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
    </tr>
    <tr>
      <th>1072</th>
      <td>1</td>
      <td>28</td>
      <td>28000</td>
      <td>2800000000</td>
      <td>인천광역시</td>
      <td>인천광역시</td>
      <td>인천광역시</td>
    </tr>
    <tr>
      <th>2111</th>
      <td>1</td>
      <td>41</td>
      <td>41000</td>
      <td>4100000000</td>
      <td>경기도</td>
      <td>경기도</td>
      <td>경기도</td>
    </tr>
  </tbody>
</table>
</div>



DM_STTNBY_USECNT_T 테이블은 용량이 41.42GB로 Jupyter Notebook으로 한 번에 불러오기에는 애로 사항이 있어 한 줄씩 불러오면서 필터링을 진행했습니다. 19년 데이터와 20년 데이터를 나누어 저장했습니다. 


```python
card_filtered19, card_filtered20 = [], []
columns = ['년도','년월','운행 일자','요일 구분','시간대','이용자 유형 코드','정산사 ID','정산 지역 코드',
           '교통수단 구분 코드','정류장 ID','시도 코드','시군구 코드','이용 지역 코드','승차 인원','하차 인원'] # 정의서에 적혀있는 column 명칭
with open('data/card/CARD_0002/DM_STTNBY_USECNT_T.dat', 'r') as read_obj:
    csv_reader = reader(read_obj, delimiter = "|")
    for row in csv_reader:
        if row[12] != '9999999999': # 비정상적 이용 지역 코드는 card_filtered에 저장하지 않음
            if row[8] == "T": # 교통수단 구분 코드가 지하철인 경우에만 card_filtered에 저장 
                if row[10] in ['11', '28', '41']: # 시도 코드가 서울특별시, 경기도, 인천광역시인 경우에만 card_filtered에 저장
                    if row[0] == '2019':
                        card_filtered19.append(row)
                    elif row[0] == '2020':   
                        card_filtered20.append(row)
                        
card_filtered19 = pd.DataFrame(card_filtered19)
card_filtered19.columns = columns 
card_filtered20 = pd.DataFrame(card_filtered20)
card_filtered20.columns = columns 
```

또한 추후 편의성과 효율성을 위해서 필요하지 않다고 생각되는 column들을 삭제 조치하였습니다. 


```python
for col in ["년월","요일 구분", "정산사 ID", "정산 지역 코드", "교통수단 구분 코드", "시군구 코드", "이용 지역 코드"]:
    del card_filtered19[col], card_filtered20[col]
card_filtered19.to_csv("data/additional/Card_CapitalArea_Subway_2019.csv", index = False, encoding="utf-8") 
card_filtered20.to_csv("data/additional/Card_CapitalArea_Subway_2020.csv", index = False, encoding="utf-8") 
```

### <u>Step 3. '날짜 인덱스' column 생성</u>
정류장별 이용자수는 요일에 영향을 받습니다. 예를 들어 같은 3월 2일이라고 하더라도 2019년 3월 2일은 토요일이었고 2020년 3월 2일은 월요일이었기 때문에 정류장별 이용자수 패턴이 다를 확률이 높습니다. 2020년과 2019년의 정확한 일대일비교를 위해선 날짜만 비교하는 것이 아니라 요일도 고려하여 비교를 해야합니다. 이 문제를 해결하기 위해서 '날짜 인덱스'라는 column을 추가하였습니다. 

'날짜 인덱스' column을 생성한 방식은 다음과 같습니다. 
* 월요일이 1이라는 기준하에 2019년 1월 1일은 화요일이었기에 2를 배정하였습니다. 하루가 지날수록 1 더 큰 숫자를 배정하였습니다. 예를 들어 2019년 1월 2일은 3, 1월 3일은 4... 이런 방식입니다. 본 데이터에는 없지만 2019년 12월 31일이 있었더라면 366을 배정받았을 것입니다. 
* 마찬가지로 월요일이 1이라는 기준하에 2020년 1월 1일은 수요일이었기에 3을 배정하였습니다. 1월 2일은 4, 1월 3일은 5... 등 같은 방식으로 배정했습니다. 
* 날짜가 아닌 이렇게 생성된 '날짜 인덱스' column을 기준으로 비교하였을 경우 날짜와 요일을 복합적으로 고려하여 2019년, 2020년의 동일 종류의 데이터를 비교할 수 있다는 장점이 있습니다.

추가적으로 평일과 주말을 구분하는 '요일 구분' column도 생성하였습니다. 
### 1. 2019년, 2020년 날짜 인덱스 생성


```python
for year in ['2019', '2020']: 
    card_filtered = pd.read_csv("data/additional/Card_CapitalArea_Subway_"+year+".csv")
    if year == '2019':
        start_num = 1 # 2019년 1월 1일은 화요일이었기 때문에 start_num이 1입니다 
    else: 
        start_num = 2 # 2020년 1월 1일은 수요일이었기 때문에 start_num이 2입니다
    date_index, weekend = [], []
    dates = card_filtered["운행 일자"].unique()
    for i in dates:
        date_index.append(datetime.strptime(str(i), '%Y%m%d').timetuple().tm_yday+start_num) # 주어진 운행일자가 해당 년도의 몇 번째 날인지 구하고 start_num를 더합니다
        if (date_index[-1]-1) % 7 <= 4:
            weekend.append("평일")
        else: 
            weekend.append("주말")
    card_filtered["날짜 인덱스"] = card_filtered["운행 일자"].replace(dates, date_index)
    card_filtered["요일 구분"] = card_filtered["날짜 인덱스"].replace(date_index, weekend)
    card_filtered.to_csv("data/additional/Card_CapitalArea_Subway_"+year+".csv", index = False, encoding="utf-8")
```

### 2. 2019년 데이터와 2020년 데이터 합치기
기존의 데이터는 2019년과 2020년 데이터가 서로 다른 row로 구분이 되어있었습니다.불필요한 용량을 줄이기 위해서 시도 코드, 정류장 ID, 날짜 인덱스, 시간대, 이용자 유형 코드를 기준으로 하여 2019년 데이터와 2020년 데이터를 합쳤습니다. 이를 통해 같은 row에서 19년도 승차인원, 19년도 하차인원, 20년도 승차인원, 20년도 하차인원을 쉽게 확인, 비교할 수 있게 되었습니다.

Card_CapitalArea_Subway_combined.csv로 저장하였으며 추후 Tableau에서 visualization을 생성할시 사용되는 파일입니다. 


```python
card_filtered19 = pd.read_csv("data/additional/Card_CapitalArea_Subway_2019.csv") 
card_filtered20 = pd.read_csv("data/additional/Card_CapitalArea_Subway_2020.csv") 
combined = pd.merge(card_filtered19, card_filtered20, how = 'inner',
                    on = ["시도 코드","정류장 ID","날짜 인덱스","시간대","이용자 유형 코드"], suffixes=['_19','_20'])
del combined["년도_19"], combined["년도_20"], combined["요일 구분_19"]
combined.columns = ['운행 일자_19', '시간대', '이용자 유형 코드', '정류장 ID', '시도 코드', '승차 인원_19',
       '하차 인원_19', '날짜 인덱스', '운행 일자_20', '승차 인원_20', '하차 인원_20', '요일 구분']
combined.to_csv("data/additional/Card_CapitalArea_Subway_combined.csv", index = False, encoding="utf-8")
combined.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자_19</th>
      <th>시간대</th>
      <th>이용자 유형 코드</th>
      <th>정류장 ID</th>
      <th>시도 코드</th>
      <th>승차 인원_19</th>
      <th>하차 인원_19</th>
      <th>날짜 인덱스</th>
      <th>운행 일자_20</th>
      <th>승차 인원_20</th>
      <th>하차 인원_20</th>
      <th>요일 구분</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190102</td>
      <td>0</td>
      <td>1</td>
      <td>1809</td>
      <td>28</td>
      <td>36</td>
      <td>252</td>
      <td>3</td>
      <td>20200101</td>
      <td>28</td>
      <td>114</td>
      <td>평일</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190102</td>
      <td>0</td>
      <td>1</td>
      <td>1810</td>
      <td>28</td>
      <td>3</td>
      <td>125</td>
      <td>3</td>
      <td>20200101</td>
      <td>3</td>
      <td>69</td>
      <td>평일</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190102</td>
      <td>0</td>
      <td>1</td>
      <td>1823</td>
      <td>28</td>
      <td>2</td>
      <td>47</td>
      <td>3</td>
      <td>20200101</td>
      <td>0</td>
      <td>32</td>
      <td>평일</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190102</td>
      <td>0</td>
      <td>1</td>
      <td>1888</td>
      <td>28</td>
      <td>5</td>
      <td>34</td>
      <td>3</td>
      <td>20200101</td>
      <td>0</td>
      <td>29</td>
      <td>평일</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190102</td>
      <td>0</td>
      <td>1</td>
      <td>1889</td>
      <td>28</td>
      <td>0</td>
      <td>22</td>
      <td>3</td>
      <td>20200101</td>
      <td>0</td>
      <td>8</td>
      <td>평일</td>
    </tr>
  </tbody>
</table>
</div>



###  <u>Step 4. DM_STTN_T (정류장) 테이블 필터링</u>
DM_STTNBY_USECNT_T 테이블에는 정류장 ID는 있지만 정류장 명칭을 알 수 없습니다. 정류장 명칭을 알기 위해서는 제공 받은 '한국교통안전공단 교통카드 데이터' 중 DM_STTN_T (정류장) 테이블을 사용해야합니다. 

Step 2해서 했던 필터링과 마찬가지로 수도권 지하철역만 필터링했습니다.


```python
STTN = pd.read_csv("data/card/CARD_0001/DM_STTN_T.dat", sep='|', header=None)
STTN.columns = ['운행 일자', '정산사 ID','정산 지역 코드','교통수단 구분 코드','정류장 ID',
                '정류장 명칭','정류장 ARS번호', '시도 코드','시군구 코드','이용 지역 코드','노선 수'] 
STTN = STTN[STTN["교통수단 구분 코드"] == "T"] # 지하철역만 선택 
STTN = STTN[STTN["시도 코드"].isin(['11', '28', '41'])] # 수도권만 선택 
STTN.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46170</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>150</td>
      <td>서울역 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114012000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>46171</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>151</td>
      <td>시청 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114016700</td>
      <td>1</td>
    </tr>
    <tr>
      <th>46172</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>152</td>
      <td>종각 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111013500</td>
      <td>1</td>
    </tr>
    <tr>
      <th>46173</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>153</td>
      <td>종로3가 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111015600</td>
      <td>1</td>
    </tr>
    <tr>
      <th>46174</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>154</td>
      <td>종로5가 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111016300</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



또한 card_filtered19, card_filtered20에 있는 정류장만 필터링해 남겼습니다. 


```python
STTN_filtered = [] 
for index, row in pd.concat([card_filtered19, card_filtered20]).drop_duplicates(["정류장 ID", "시도 코드"]).iterrows(): 
    temp = STTN[STTN["정류장 ID"] == int(row["정류장 ID"])]
    temp = temp[temp["시도 코드"] == int(row["시도 코드"])].reset_index(drop = True)
    STTN_filtered.append(temp.iloc[0])
STTN_filtered = pd.DataFrame(STTN_filtered).drop_duplicates(["정류장 ID", "시도 코드"])
STTN_filtered.shape
```




    (698, 11)



필터링 후 698개의 지하철역이 남았습니다. 이 698개의 역을 서울, 경기, 인천 지역별로 나누어 저장했습니다. 


```python
region_code_dict = {"Seoul":11, "Incheon":28, "Gyeonggi":41}
for region in region_code_dict:
    temp = STTN_filtered[STTN_filtered["시도 코드"] == region_code_dict[region]]
    temp.to_csv('data/additional/sttn_index_'+region+'.csv', index = False, encoding = "utf-8")
```

### <u>Step 5. 역이름 → 도로명 주소 (Selenium, Web Scraping)</u>
Step 5의 경우 데이터 처리 후 검토과정이 많이 필요했던 작업이었습니다. DM_STTN_T 테이블을 이용하여 각 정류장 ID에 대응되는 정류장 명칭을 찾을 수 있었으나 지도에 정류장을 표시하기 위해서는 위도, 경도가 필요했습니다. Naver Map이나 Kakao Map API를 사용하여 역이름을 검색하면 위도, 경도 정보를 받을 수 있을 것이라고 예상했지만, 도로명 주소를 정확히 입력했을시에만 위도, 경도를 제공해준다는 사실을 알게 되었습니다. 

이 문제를 해결하기 위해 역이름에서 위도, 경도를 찾는 1단계 방식이 아닌 (1) 역이름을 통해서 도로명 주소를 찾고 (2) 도로명 주소를 통해서 위도, 경도를 찾는 2단계 접근법을 사용하였습니다. 본 Step 5는 그 2단계 접근법의 첫 번째 단계이며 Selenium을 사용하여 네이버 지도 서비스의 Web Scraping을 진행하였습니다. findStreetAddress 함수의 코드는 Step 0에서 확인하실 수 있습니다. 
### 1. 인천 지하철역 도로명 주소 구하기


```python
STTN_filtered_Incheon = pd.read_csv("data/additional/sttn_index_Incheon.csv")
STTN_filtered_Incheon = findStreetAddress(STTN_filtered_Incheon)
STTN_filtered_Incheon.to_csv("data/additional/sttn_index_Incheon_with_address.csv", index = False, encoding="utf-8")
STTN_filtered_Incheon.head()
```

    [WDM] - Current google-chrome version is 85.0.4183
    [WDM] - Get LATEST driver version for 85.0.4183
    [WDM] - There is no [mac64] chromedriver for browser 85.0.4183 in cache
    [WDM] - Get LATEST driver version for 85.0.4183
    [WDM] - Trying to download new driver from http://chromedriver.storage.googleapis.com/85.0.4183.87/chromedriver_mac64.zip


     


    [WDM] - Driver has been saved in cache [/Users/junhwalee/.wdm/drivers/chromedriver/mac64/85.0.4183.87]





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1809</td>
      <td>주안 [1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710500</td>
      <td>1</td>
      <td>주안역 1호선</td>
      <td>주안역 1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 주안로 95-19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1810</td>
      <td>제물포 [1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710400</td>
      <td>1</td>
      <td>제물포역 1호선</td>
      <td>제물포역 1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 경인로 129</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1823</td>
      <td>도화 [1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710400</td>
      <td>1</td>
      <td>도화역 1호선</td>
      <td>도화역 1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 숙골로24번길 9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1888</td>
      <td>인하대 [수인선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710200</td>
      <td>1</td>
      <td>인하대역 수인선</td>
      <td>인하대역 수인선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 독배로 313</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1889</td>
      <td>숭의 [수인선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710200</td>
      <td>1</td>
      <td>숭의역 수인선</td>
      <td>숭의역 수인선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 숭의동 379-72</td>
    </tr>
  </tbody>
</table>
</div>



리퀘스트를 너무 많이 보냈거나 인터넷 환경에 따라 깨지는 경우가 간혹 발생하기도 합니다. 또한 잘못된 검색 결과가 나오는 경우도 있어 사람의 눈으로 검토하는 과정이 필요합니다. 검토 및 수정 후 sttn_index_Incheon_with_address_reviewed이라는 이름의 별도의 csv로 저장하였습니다. 


```python
STTN_filtered_Incheon = pd.read_csv("data/additional/sttn_index_Incheon_with_address_reviewed.csv")
print(STTN_filtered_Incheon.shape)
for col in ["정류장 명칭", "Sel 검색명칭","Sel 검색결과", "Sel 카테고리", "Sel 주소"]:
    print(col + ": " + str(STTN_filtered_Incheon[col].nunique()))
```

    (89, 15)
    정류장 명칭: 89
    Sel 검색명칭: 89
    Sel 검색결과: 89
    Sel 카테고리: 1
    Sel 주소: 81


sttn_index_Incheon_with_address_reviewed를 확인하였을 때 89개의 row가 있었고 89개의 '정류장 명칭'이 있었습니다. 'Sel 검색명칭'도 89가지, 'Sel 검색결과'도 89가지가 있는 것을 보았을 때 Web Scraping과 검토를 통해서 데이터가 잘 정리된 것이라 볼 수 있습니다. 또한 'Sel 카테고리'도 '지하철, 전철'로 통일이 되었습니다. 

하지만 '정류장 명칭'은 89가지이지만 'Sel 주소'는 81개에 불과합니다. 그 이유를 알아봤습니다. 'Sel 주소'가 겹치는 데이터를 샘플로 몇 가지만 알아보면 다음과 같습니다.  


```python
STTN_filtered_Incheon[STTN_filtered_Incheon.duplicated("Sel 주소", keep = False)].sort_values("Sel 주소").head(6)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>21</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1884</td>
      <td>원인재 [수인선]</td>
      <td>~</td>
      <td>28</td>
      <td>28185</td>
      <td>2818510300</td>
      <td>1</td>
      <td>원인재역 수인선</td>
      <td>원인재역 수인선</td>
      <td>지하철,전철</td>
      <td>인천 연수구 벚꽃로 195</td>
    </tr>
    <tr>
      <th>48</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>3130</td>
      <td>원인재 [인천1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28185</td>
      <td>2818510300</td>
      <td>1</td>
      <td>원인재역 인천1호선</td>
      <td>원인재역 인천1호선</td>
      <td>지하철,전철</td>
      <td>인천 연수구 벚꽃로 195</td>
    </tr>
    <tr>
      <th>29</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>3110</td>
      <td>계양 [인천1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28245</td>
      <td>2824511100</td>
      <td>1</td>
      <td>계양역 인천1호선</td>
      <td>계양역 인천1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 계양구 귤현동 451-475</td>
    </tr>
    <tr>
      <th>81</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>4208</td>
      <td>계양 [공항철도]</td>
      <td>~</td>
      <td>28</td>
      <td>28245</td>
      <td>2824511100</td>
      <td>1</td>
      <td>계양역 공항철도</td>
      <td>계양역 공항철도</td>
      <td>지하철,전철</td>
      <td>인천광역시 계양구 귤현동 451-475</td>
    </tr>
    <tr>
      <th>43</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>3124</td>
      <td>인천시청 [인천1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28200</td>
      <td>2820010200</td>
      <td>1</td>
      <td>인천시청역 인천1호선</td>
      <td>인천시청역 인천1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 남동구 예술로 264 금영쉐르빌</td>
    </tr>
    <tr>
      <th>74</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>3221</td>
      <td>인천시청 [인천2호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28200</td>
      <td>2820010200</td>
      <td>1</td>
      <td>인천시청역 인천2호선</td>
      <td>인천시청역 인천2호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 남동구 예술로 264 금영쉐르빌</td>
    </tr>
  </tbody>
</table>
</div>



위에서 볼 수 있듯이 역은 겹치지만 호선이 겹치지 않아 다른 정류장으로 구분되어진 사례들입니다. 이와 같이 호선에 상관없이 각 역마다 하나의 주소를 가지는 것이 옳습니다. 

하지만 호선이 다르다는 이유로 같은 역임에도 다른 주소가 배정된 케이스가 있을 수도 있습니다. 이를 확인하고 해결하기 위해 아래와 같은 코드를 통해 'Sel 역명'이라는 column을 새로 생성해 호선에 상관없이 같은 역이라면 같은 주소를 배정했습니다.  


```python
sttn_without_line = []
for index, row in STTN_filtered_Incheon.iterrows():
    sttn_without_line.append(row["Sel 검색결과"].split(" ")[0])
STTN_filtered_Incheon["Sel 역명"] = sttn_without_line
STTN_filtered_Incheon.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
      <th>Sel 역명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1809</td>
      <td>주안 [1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710500</td>
      <td>1</td>
      <td>주안역 1호선</td>
      <td>주안역 1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 주안로 95-19</td>
      <td>주안역</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1810</td>
      <td>제물포 [1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710400</td>
      <td>1</td>
      <td>제물포역 1호선</td>
      <td>제물포역 1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 경인로 129</td>
      <td>제물포역</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1823</td>
      <td>도화 [1호선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710400</td>
      <td>1</td>
      <td>도화역 1호선</td>
      <td>도화역 1호선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 숙골로24번길 9</td>
      <td>도화역</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1888</td>
      <td>인하대 [수인선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710200</td>
      <td>1</td>
      <td>인하대역 수인선</td>
      <td>인하대역 수인선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 독배로 313</td>
      <td>인하대역</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1889</td>
      <td>숭의 [수인선]</td>
      <td>~</td>
      <td>28</td>
      <td>28177</td>
      <td>2817710200</td>
      <td>1</td>
      <td>숭의역 수인선</td>
      <td>숭의역 수인선</td>
      <td>지하철,전철</td>
      <td>인천광역시 미추홀구 숭의동 379-72</td>
      <td>숭의역</td>
    </tr>
  </tbody>
</table>
</div>




```python
for index, row in STTN_filtered_Incheon.iterrows():
    temp = STTN_filtered_Incheon.drop_duplicates(["Sel 역명"])
    temp = temp[temp["Sel 역명"] == row["Sel 역명"]]
    STTN_filtered_Incheon.loc[index,"Sel 주소"] = temp.iloc[0]["Sel 주소"]
STTN_filtered_Incheon.to_csv("data/additional/sttn_index_Incheon_with_address_reviewed.csv", index = False, encoding="utf-8")
```


```python
STTN_filtered_Incheon["Sel 역명"].nunique() == STTN_filtered_Incheon["Sel 주소"].nunique() # 'Sel 주소'의 갯수와 'Sel 역명'의 개수가 일치 확인
```




    True



### 2. 경기 지하철역 도로명 주소 구하기


```python
STTN_filtered_Gyeonggi = pd.read_csv('data/additional/sttn_index_Gyeonggi.csv')
STTN_filtered_Gyeonggi = findStreetAddress(STTN_filtered_Gyeonggi)
STTN_filtered_Gyeonggi.to_csv("data/additional/sttn_index_Gyeonggi_with_address.csv", index = False, encoding="utf-8")
STTN_filtered_Gyeonggi.head()
```

    [WDM] - Current google-chrome version is 84.0.4147
    [WDM] - Get LATEST driver version for 84.0.4147
    [WDM] - Driver [/Users/junhwalee/.wdm/drivers/chromedriver/mac64/84.0.4147.30/chromedriver] found in cache


     





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1205</td>
      <td>구리 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41310</td>
      <td>4131010300</td>
      <td>1</td>
      <td>구리역 경의중앙선</td>
      <td>구리역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 구리시 건원대로34번길 32-29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1206</td>
      <td>도농 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136011200</td>
      <td>1</td>
      <td>도농역 경의중앙선</td>
      <td>도농역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 경춘로 433 도농역</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1207</td>
      <td>양정 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136010500</td>
      <td>1</td>
      <td>양정역 경의중앙선</td>
      <td>양정역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 경강로 237 양정역</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1208</td>
      <td>덕소 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136025021</td>
      <td>1</td>
      <td>덕소역 경의중앙선</td>
      <td>덕소역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 와부읍 덕소로 56 덕소역</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1209</td>
      <td>도심 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136025022</td>
      <td>1</td>
      <td>도심역 경의중앙선</td>
      <td>도심역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 와부읍 덕소로 237</td>
    </tr>
  </tbody>
</table>
</div>



리퀘스트를 너무 많이 보냈거나 인터넷 환경에 따라 깨지는 경우가 간혹 발생하기도 합니다. 또한 잘못된 검색 결과가 나오는 경우도 있어 사람의 눈으로 검토하는 과정이 필요합니다. 검토 및 수정 후 sttn_index_Gyeonggi_with_address_reviewed이라는 이름의 별도의 csv로 저장하였습니다. 


```python
STTN_filtered_Gyeonggi = pd.read_csv("data/additional/sttn_index_Gyeonggi_with_address_reviewed.csv")
print(STTN_filtered_Gyeonggi.shape)
for col in ["정류장 명칭", "Sel 검색명칭","Sel 검색결과", "Sel 카테고리", "Sel 주소"]:
    print(col + ": " + str(STTN_filtered_Gyeonggi[col].nunique()))
```

    (229, 15)
    정류장 명칭: 228
    Sel 검색명칭: 228
    Sel 검색결과: 228
    Sel 카테고리: 1
    Sel 주소: 218


sttn_index_Gyeonggi_with_address_reviewed를 확인하였을 때 229개의 row가 있습니다. 'Sel 카테고리'도 '지하철, 전철' 하나로 통일이 되었습니다. 하지만 '정류장 명칭', 'Sel 검색명칭', 'Sel 검색결과'는 하나가 부족한 228개입니다.   


```python
STTN_filtered_Gyeonggi[STTN_filtered_Gyeonggi.duplicated(["정류장 명칭", "Sel 검색명칭", "Sel 검색결과"], keep = False)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>184</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>309</td>
      <td>지축 [3호선]</td>
      <td>~</td>
      <td>41</td>
      <td>41281</td>
      <td>4128110900</td>
      <td>1</td>
      <td>지축역 3호선</td>
      <td>지축역 3호선</td>
      <td>지하철,전철</td>
      <td>경기도 고양시 덕양구 삼송로 300</td>
    </tr>
    <tr>
      <th>219</th>
      <td>20190323</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1949</td>
      <td>지축 [3호선]</td>
      <td>~</td>
      <td>41</td>
      <td>41281</td>
      <td>4128110900</td>
      <td>1</td>
      <td>지축역 3호선</td>
      <td>지축역 3호선</td>
      <td>지하철,전철</td>
      <td>경기도 고양시 덕양구 삼송로 300</td>
    </tr>
  </tbody>
</table>
</div>



그 이유는 위에서 볼 수 있듯이 지축역에 배정된 정류장 ID가 309, 1949 총 두 가지이기 때문입니다. 데이터상 그러한 모습을 보일뿐 현대 코드 구성상 문제가 되지는 않습니다. 

또 다른 문제는 '정류장 명칭'은 229가지이지만 'Sel 주소'는 218가지에 불과하다는겁니다. 그 이유를 알아봤습니다. 'Sel 주소'가 겹치는 데이터를 샘플로 몇 가지만 알아보면 다음과 같습니다.


```python
STTN_filtered_Gyeonggi[STTN_filtered_Gyeonggi.duplicated("Sel 주소", keep = False)].sort_values("Sel 주소").head(6)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>219</th>
      <td>20190323</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1949</td>
      <td>지축 [3호선]</td>
      <td>~</td>
      <td>41</td>
      <td>41281</td>
      <td>4128110900</td>
      <td>1</td>
      <td>지축역 3호선</td>
      <td>지축역 3호선</td>
      <td>지하철,전철</td>
      <td>경기도 고양시 덕양구 삼송로 300</td>
    </tr>
    <tr>
      <th>184</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>309</td>
      <td>지축 [3호선]</td>
      <td>~</td>
      <td>41</td>
      <td>41281</td>
      <td>4128110900</td>
      <td>1</td>
      <td>지축역 3호선</td>
      <td>지축역 3호선</td>
      <td>지하철,전철</td>
      <td>경기도 고양시 덕양구 삼송로 300</td>
    </tr>
    <tr>
      <th>165</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>4804</td>
      <td>소사 [서해선]</td>
      <td>~</td>
      <td>41</td>
      <td>41190</td>
      <td>4119011000</td>
      <td>1</td>
      <td>소사역 서해선</td>
      <td>소사역 서해선</td>
      <td>지하철,전철</td>
      <td>경기도 부천시 경인로 363</td>
    </tr>
    <tr>
      <th>84</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1814</td>
      <td>소사 [1호선]</td>
      <td>~</td>
      <td>41</td>
      <td>41190</td>
      <td>4119011000</td>
      <td>1</td>
      <td>소사역 1호선</td>
      <td>소사역 1호선</td>
      <td>지하철,전철</td>
      <td>경기도 부천시 경인로 363</td>
    </tr>
    <tr>
      <th>94</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1858</td>
      <td>미금 [분당선]</td>
      <td>~</td>
      <td>41</td>
      <td>41135</td>
      <td>4113511400</td>
      <td>1</td>
      <td>미금역 분당선</td>
      <td>미금역 분당선</td>
      <td>지하철,전철</td>
      <td>경기도 성남시 분당구 성남대로 156</td>
    </tr>
    <tr>
      <th>201</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>4313</td>
      <td>미금 [신분당선]</td>
      <td>~</td>
      <td>41</td>
      <td>41135</td>
      <td>4113511400</td>
      <td>1</td>
      <td>미금역 신분당선</td>
      <td>미금역 신분당선</td>
      <td>지하철,전철</td>
      <td>경기도 성남시 분당구 성남대로 156</td>
    </tr>
  </tbody>
</table>
</div>



인천 데이터와 마찬가지로 역은 겹치지만 호선이 겹치지 않아 다른 정류장으로 구분되어진 사례들입니다. 이와 같이 호선에 상관없이 각 역마다 하나의 주소를 가지는 것이 옳습니다. 

하지만 호선이 다르다는 이유로 같은 역임에도 다른 주소가 배정된 케이스가 있을 수도 있습니다. 이를 확인하고 해결하기 위해 아래와 같은 코드를 통해 'Sel 역명'이라는 column을 새로 생성해 호선에 상관없이 같은 역이라면 같은 주소를 배정했습니다.  


```python
sttn_without_line = []
for index, row in STTN_filtered_Gyeonggi.iterrows():
    sttn_without_line.append(row["Sel 검색결과"].split(" ")[0])
STTN_filtered_Gyeonggi["Sel 역명"] = sttn_without_line
STTN_filtered_Gyeonggi.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
      <th>Sel 역명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1205</td>
      <td>구리 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41310</td>
      <td>4131010300</td>
      <td>1</td>
      <td>구리역 경의중앙선</td>
      <td>구리역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 구리시 건원대로34번길 32-29</td>
      <td>구리역</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1206</td>
      <td>도농 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136011200</td>
      <td>1</td>
      <td>도농역 경의중앙선</td>
      <td>도농역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 경춘로 433 도농역</td>
      <td>도농역</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1207</td>
      <td>양정 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136010500</td>
      <td>1</td>
      <td>양정역 경의중앙선</td>
      <td>양정역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 경강로 237 양정역</td>
      <td>양정역</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1208</td>
      <td>덕소 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136025021</td>
      <td>1</td>
      <td>덕소역 경의중앙선</td>
      <td>덕소역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 와부읍 덕소로 56 덕소역</td>
      <td>덕소역</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1209</td>
      <td>도심 [경의중앙선]</td>
      <td>~</td>
      <td>41</td>
      <td>41360</td>
      <td>4136025022</td>
      <td>1</td>
      <td>도심역 경의중앙선</td>
      <td>도심역 경의중앙선</td>
      <td>지하철,전철</td>
      <td>경기도 남양주시 와부읍 덕소로 237</td>
      <td>도심역</td>
    </tr>
  </tbody>
</table>
</div>




```python
for index, row in STTN_filtered_Gyeonggi.iterrows():
    temp = STTN_filtered_Gyeonggi.drop_duplicates(["Sel 역명"])
    temp = temp[temp["Sel 역명"] == row["Sel 역명"]]
    STTN_filtered_Gyeonggi.loc[index,"Sel 주소"] = temp.iloc[0]["Sel 주소"]
STTN_filtered_Gyeonggi.to_csv("data/additional/sttn_index_Gyeonggi_with_address_reviewed.csv", index = False)
```


```python
STTN_filtered_Gyeonggi["Sel 역명"].nunique() == STTN_filtered_Gyeonggi["Sel 주소"].nunique() # 'Sel 주소'의 갯수와 'Sel 역명'의 개수가 일치 확인
```




    True



### 3. 서울 지하철역 도로명 주소 구하기


```python
STTN_filtered_Seoul = pd.read_csv('data/additional/sttn_index_Seoul.csv')
STTN_filtered_Seoul = findStreetAddress(STTN_filtered_Seoul)
STTN_filtered_Seoul.to_csv("data/additional/sttn_index_Seoul_with_address.csv", index = False, encoding="utf-8")
STTN_filtered_Seoul.head()
```

    [WDM] - Current google-chrome version is 84.0.4147
    [WDM] - Get LATEST driver version for 84.0.4147
    [WDM] - Driver [/Users/junhwalee/.wdm/drivers/chromedriver/mac64/84.0.4147.30/chromedriver] found in cache


     





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>150</td>
      <td>서울역 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114012000</td>
      <td>1</td>
      <td>서울역역 1호선</td>
      <td>서울역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 중구 세종대로 2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>151</td>
      <td>시청 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114016700</td>
      <td>1</td>
      <td>시청역 1호선</td>
      <td>시청역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 중구 세종대로 101</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>152</td>
      <td>종각 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111013500</td>
      <td>1</td>
      <td>종각역 1호선</td>
      <td>종각역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 종로구 종로 55 종로 55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>153</td>
      <td>종로3가 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111015600</td>
      <td>1</td>
      <td>종로3가역 1호선</td>
      <td>종로3가역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 종로구 종로 129 종로 129</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>154</td>
      <td>종로5가 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111016300</td>
      <td>1</td>
      <td>종로5가역 1호선</td>
      <td>종로5가역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 종로구 종로 216 종로 216</td>
    </tr>
  </tbody>
</table>
</div>



리퀘스트를 너무 많이 보냈거나 인터넷 환경에 따라 깨지는 경우가 간혹 발생하기도 합니다. 또한 잘못된 검색 결과가 나오는 경우도 있어 사람의 눈으로 검토하는 과정이 필요합니다. 검토 및 수정 후 sttn_index_Seoul_with_address_reviewed이라는 이름의 별도의 csv로 저장하였습니다. 


```python
STTN_filtered_Seoul = pd.read_csv("data/additional/sttn_index_Seoul_with_address_reviewed.csv")
print(STTN_filtered_Seoul.shape)
for col in ["정류장 명칭", "Sel 검색명칭","Sel 검색결과", "Sel 카테고리", "Sel 주소"]:
    print(col + ": " + str(STTN_filtered_Seoul[col].nunique()))
```

    (380, 15)
    정류장 명칭: 379
    Sel 검색명칭: 379
    Sel 검색결과: 379
    Sel 카테고리: 1
    Sel 주소: 299


sttn_index_Seoul_with_address_reviewed를 확인하였을 때 380개의 row가 있습니다. 'Sel 카테고리'도 '지하철, 전철' 하나로 통일이 되었습니다. 하지만 '정류장 명칭', 'Sel 검색명칭', 'Sel 검색결과'는 하나가 부족한 379개입니다.   


```python
STTN_filtered_Seoul[STTN_filtered_Seoul.duplicated(["정류장 명칭", "Sel 검색명칭", "Sel 검색결과"], keep = False)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>150</td>
      <td>서울역 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114012000</td>
      <td>1</td>
      <td>서울역역 1호선</td>
      <td>서울역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 중구 세종대로 2</td>
    </tr>
    <tr>
      <th>85</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1001</td>
      <td>서울역 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114012000</td>
      <td>1</td>
      <td>서울역역 1호선</td>
      <td>서울역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 중구 세종대로 2</td>
    </tr>
  </tbody>
</table>
</div>



그 이유는 위에서 볼 수 있듯이 서울역에 배정된 정류장 ID가 150, 1001 총 두 가지이기 때문입니다. 데이터상 그러한 모습을 보일뿐 현대 코드 구성상 문제가 되지는 않습니다. 

또 다른 문제는 '정류장 명칭'은 379가지이지만 'Sel 주소'는 299가지에 불과하다는겁니다. 그 이유를 알아봤습니다. 'Sel 주소'가 겹치는 데이터 몇 가지를 샘플로 알아보면 다음과 같습니다.


```python
STTN_filtered_Seoul[STTN_filtered_Seoul.duplicated("Sel 주소", keep = False)].sort_values("Sel 주소").head(6)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>138</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1850</td>
      <td>선정릉 [분당선]</td>
      <td>~</td>
      <td>11</td>
      <td>11680</td>
      <td>1168010500</td>
      <td>1</td>
      <td>선정릉역 분당선</td>
      <td>선정릉역 분당선</td>
      <td>지하철,전철</td>
      <td>서울 강남구 선릉로 580</td>
    </tr>
    <tr>
      <th>285</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>4127</td>
      <td>선정릉 [9호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11680</td>
      <td>1168010800</td>
      <td>1</td>
      <td>선정릉역 9호선</td>
      <td>선정릉역 9호선</td>
      <td>지하철,전철</td>
      <td>서울 강남구 선릉로 580</td>
    </tr>
    <tr>
      <th>235</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>2732</td>
      <td>강남구청 [7호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11680</td>
      <td>1168010500</td>
      <td>1</td>
      <td>강남구청역 7호선</td>
      <td>강남구청역 7호선</td>
      <td>지하철,전철</td>
      <td>서울 강남구 학동로 346</td>
    </tr>
    <tr>
      <th>137</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>1849</td>
      <td>강남구청 [분당선]</td>
      <td>~</td>
      <td>11</td>
      <td>11680</td>
      <td>1168010400</td>
      <td>1</td>
      <td>강남구청역 분당선</td>
      <td>강남구청역 분당선</td>
      <td>지하철,전철</td>
      <td>서울 강남구 학동로 346</td>
    </tr>
    <tr>
      <th>379</th>
      <td>20200101</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>4929</td>
      <td>김포공항 [김포도시철도]</td>
      <td>~</td>
      <td>11</td>
      <td>11500</td>
      <td>1150010900</td>
      <td>1</td>
      <td>김포공항역 김포도시철도</td>
      <td>김포공항역 김포골드라인</td>
      <td>지하철,전철</td>
      <td>서울 강서구 하늘길 77</td>
    </tr>
    <tr>
      <th>299</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>4207</td>
      <td>김포공항 [공항철도]</td>
      <td>~</td>
      <td>11</td>
      <td>11500</td>
      <td>1150010900</td>
      <td>1</td>
      <td>김포공항역 공항철도</td>
      <td>김포공항역 공항철도</td>
      <td>지하철,전철</td>
      <td>서울 강서구 하늘길 77</td>
    </tr>
  </tbody>
</table>
</div>



위에서 볼 수 있듯이 역은 겹치지만 호선이 겹치지 않아 다른 정류장으로 구분되어진 사례들입니다. 이와 같이 호선에 상관없이 각 역마다 하나의 주소를 가지는 것이 옳습니다. 

하지만 호선이 다르다는 이유로 같은 역임에도 다른 주소가 배정된 케이스가 있을 수도 있습니다. 이를 확인하고 해결하기 위해 아래와 같은 코드를 통해 'Sel 역명'이라는 column을 새로 생성해 호선에 상관없이 같은 역이라면 같은 주소를 배정했습니다.  


```python
sttn_without_line = []
for index, row in STTN_filtered_Seoul.iterrows():
    sttn_without_line.append(row["Sel 검색결과"].split(" ")[0])
STTN_filtered_Seoul["Sel 역명"] = sttn_without_line
STTN_filtered_Seoul.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>운행 일자</th>
      <th>정산사 ID</th>
      <th>정산 지역 코드</th>
      <th>교통수단 구분 코드</th>
      <th>정류장 ID</th>
      <th>정류장 명칭</th>
      <th>정류장 ARS번호</th>
      <th>시도 코드</th>
      <th>시군구 코드</th>
      <th>이용 지역 코드</th>
      <th>노선 수</th>
      <th>Sel 검색명칭</th>
      <th>Sel 검색결과</th>
      <th>Sel 카테고리</th>
      <th>Sel 주소</th>
      <th>Sel 역명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>150</td>
      <td>서울역 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114012000</td>
      <td>1</td>
      <td>서울역역 1호선</td>
      <td>서울역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 중구 세종대로 2</td>
      <td>서울역</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>151</td>
      <td>시청 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11140</td>
      <td>1114016700</td>
      <td>1</td>
      <td>시청역 1호선</td>
      <td>시청역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 중구 세종대로 101</td>
      <td>시청역</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>152</td>
      <td>종각 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111013500</td>
      <td>1</td>
      <td>종각역 1호선</td>
      <td>종각역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 종로구 종로 55 종로 55</td>
      <td>종각역</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>153</td>
      <td>종로3가 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111015600</td>
      <td>1</td>
      <td>종로3가역 1호선</td>
      <td>종로3가역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 종로구 종로 129 종로 129</td>
      <td>종로3가역</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190201</td>
      <td>8</td>
      <td>11100</td>
      <td>T</td>
      <td>154</td>
      <td>종로5가 [1호선]</td>
      <td>~</td>
      <td>11</td>
      <td>11110</td>
      <td>1111016300</td>
      <td>1</td>
      <td>종로5가역 1호선</td>
      <td>종로5가역 1호선</td>
      <td>지하철,전철</td>
      <td>서울특별시 종로구 종로 216 종로 216</td>
      <td>종로5가역</td>
    </tr>
  </tbody>
</table>
</div>




```python
for index, row in STTN_filtered_Seoul.iterrows():
    temp = STTN_filtered_Seoul.drop_duplicates(["Sel 역명"])
    temp = temp[temp["Sel 역명"] == row["Sel 역명"]]
    STTN_filtered_Seoul.loc[index,"Sel 주소"] = temp.iloc[0]["Sel 주소"]
STTN_filtered_Seoul.to_csv("data/additional/sttn_index_Seoul_with_address_reviewed.csv", index = False)
```


```python
STTN_filtered_Seoul["Sel 역명"].nunique() == STTN_filtered_Seoul["Sel 주소"].nunique() # 'Sel 주소'의 갯수와 'Sel 역명'의 개수가 일치 확인
```




    True



### <u>Step 6. 도로명 주소 → 위도, 경도 (Naver Map API)</u>
Step 5에서 각 정류장에 해당하는 도로명 주소를 찾았으므로, 2단계 접근법의 두 번째 단계로 Naver Map Api를 통해 위도, 경도를 찾는 과정을 거쳤습니다. 
앞에서와 마찬가지로 인천, 경기, 서울을 나누어서 진행하였습니다. 사용한 findCoord 함수에 대한 정보는 Step 0에서 확인하시길 바랍니다. 또한 Naver Map Api를 위해 사용된 client_id와 client_secret은 개인정보로서 본 게시물에는 비공개 처리하였습니다. [Naver Cloud Platform](https://www.ncloud.com/?language=ko-KR) 회원가입 후 client_id와 client_secret을 변경한 뒤 사용하시길 바랍니다. 


```python
client_id, client_secret = "[개인정보 생략]", "[개인정보 생략]"
for region in ["Incheon", "Gyeonggi", "Seoul"]:
    STTN_filtered = pd.read_csv("data/additional/sttn_index_"+region+"_with_address_reviewed.csv")
    STTN_filtered = findCoord(STTN_filtered)
    STTN_filtered.to_csv("data/additional/sttn_index_"+region+"_with_address_coord.csv", index = False, encoding="utf-8")
```

위에서 저장한 파일들을 눈으로 검토한 뒤 각각 sttn_index_Incheon_with_address_coord_reviewed, sttn_index_Gyeonggi_with_address_coord_reviewed, sttn_index_Seoul_with_address_coord_reviewed로 저장합니다.

서울, 경기, 인천 지하철역 데이터를 합친 뒤 필요없는 column 삭제 후 수도권 지하철역 데이터를 sttn_index_full_with_address_coord.csv로 저장합니다. 이는 추후 Tableau에서 visualization을 생성할시 사용되는 파일입니다. 


```python
STTN_combined = pd.concat([pd.read_csv("data/additional/sttn_index_Seoul_with_address_coord_reviewed.csv"),
                           pd.read_csv("data/additional/sttn_index_Gyeonggi_with_address_coord_reviewed.csv"),
                           pd.read_csv("data/additional/sttn_index_Incheon_with_address_coord_reviewed.csv")])
for col in ['운행 일자', '정산사 ID', '정산 지역 코드', '교통수단 구분 코드','정류장 명칭', '정류장 ARS번호',
            '시군구 코드', '이용 지역 코드', '노선 수', 'Sel 검색명칭', 'Sel 검색결과', 'Sel 카테고리', 'Sel 주소']:
    del STTN_combined[col]
STTN_combined.to_csv("data/additional/sttn_index_full_with_address_coord.csv",
                 index = False, encoding ="utf-8")
STTN_combined.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>정류장 ID</th>
      <th>시도 코드</th>
      <th>Sel 역명</th>
      <th>long</th>
      <th>lat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>150</td>
      <td>11</td>
      <td>서울역</td>
      <td>126.972555</td>
      <td>37.557159</td>
    </tr>
    <tr>
      <th>1</th>
      <td>151</td>
      <td>11</td>
      <td>시청역</td>
      <td>126.976983</td>
      <td>37.565439</td>
    </tr>
    <tr>
      <th>2</th>
      <td>152</td>
      <td>11</td>
      <td>종각역</td>
      <td>126.983240</td>
      <td>37.570214</td>
    </tr>
    <tr>
      <th>3</th>
      <td>153</td>
      <td>11</td>
      <td>종로3가역</td>
      <td>126.992029</td>
      <td>37.570427</td>
    </tr>
    <tr>
      <th>4</th>
      <td>154</td>
      <td>11</td>
      <td>종로5가역</td>
      <td>127.001917</td>
      <td>37.570907</td>
    </tr>
  </tbody>
</table>
</div>



***

<div style="background-color:rgba(8, 14, 51, 1); text-align:center; vertical-align: middle; padding:1px 0;">
    <h2><center style = "color: white"> 분석</center></h2>
</div>

전처리 과정 중 Step 3-2에서 생성한 Card_CapitalArea_Subway_combined.csv와 Step 6에서 생성한 sttn_index_full_with_address_coord.csv, 그리고 Tableau, matplotlib를 사용하여 꼬리에 꼬리를 무는 질문을 묻고 답하는 식의 EDA 및 시각화를 진행했습니다. 

<div style="background-color:rgba(17, 30, 108, 1); text-align:center; vertical-align: middle; padding:0.5px 0;">
    <h3><b><center style = "color: white"> 1. COVID19가 지하철 이용량에 미친 영향 </center></b></h3>
</div>

COVID19의 확산이 지하철 이용량 영향에 미친 영향을 시각화하기 위해 하차인원 비율, 즉 “2020년 일자별 하차인원 수” / “2019년 일자별 하차인원 수”를 계산하였습니다. 단순히 2020년 일자별 하차인원 수의 변화만 살펴볼 경우 계절적 변동(Seasonality)과 COVID19의 영향을 분리시켜 분석할 수 없다는 한계가 있습니다. 그 한계를 극복하고 계절적 변동을 최대한 배제하여 COVID19로 인한 지하철 이용량 증가 및 감소치를 한 눈에 쉽게 확인하기 위해 19년 대비 20년의 하차인원 비율을 사용하였습니다. 


```python
display(Image('img/measure.png', unconfined = False))
```


![png](/assets/images/dacon-final_64_0.png)


이 값이 100%보다 큰 경우, 해당 일자에 2020년 지하철 이용자 수가 2019년 지하철 이용자 수보다 많았다는 것을 뜻합니다. 이와 반대로 이 값이 100%보다 작은 경우, 해당 일자에 2020년 지하철 이용자 수가 COVID19 등의 영향으로 2019년보다 적었다는 것을 뜻합니다.

<b> Q1-1. COVID19는 지하철 이용량에 어떤 영향을 주었을까? </b>


```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q1-1_?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q1-1_?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b>([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q1-1_?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 하단에 위치한 슬라이더를 이용하여 날짜에 따른 변화 트랜드를 살펴보실 수 있습니다.)</b>

날짜별로 위에 설명한 하차 인원 비율을 살펴보았습니다. 19년 날짜와 20년 날짜가 매칭이 안되는 이유는 데이터 전처리 Step 3에서 생성한 "날짜 인덱스"를 이용하였기 때문입니다. 그렇게 한 이유는 데이터 전처리 과정 Step 3에서 살펴보실 수 있습니다.  

2020년 일자별 하차인원 수와 2019년 일자별 하차인원 수가 비슷했다면 파란색 점선을 따르는 양상을 보일 것입니다. 예를 들어 전국민이 COVID19에 큰 영향을 받지 않았다고 생각되는 1월 초, 중순에는 파란색 점선을 따르는 모습을 보여주며 이는 19년과 20년 하차 인원 수가 비슷한 것을 나타냅니다. 

하지만 그 이후 그래프에선 규모가 큰 비율 차이가 발생했습니다. 큰 증감을 보인 날짜들이 2019년 설 연휴 (2월 4일 - 2월 6일)과 2020년 설 연휴 (1월 24일 - 1월 27일)인 것을 고려하였을 때 1월 말, 2월 초의 급격한 감소와 증가는 COVID19가 아니라 설날 연휴로 인한 수도권 지하철 이용객 수의 증감으로 인한 변화라는 것을 확인할 수 있었습니다. 분석 오류를 최소화하기 위해 앞으로의 분석에서는 <b>2019년 기준 2월 7일, 2020년 기준 2월 6일 이후 데이터</b>에 집중하기로 하였습니다.

그 기간의 이용량 증감폭을 살펴본 결과, 2019년에 비해 2020년에는 이용객이 눈에 띄게 감소하였다는 사실을 확인할 수 있었습니다. 특히 2월 초에는 약 10% 가량의 차이를 보이다가, 3월에 들어서는 주말 동안에는 거의 60% 전후로 이용객 수가 감소하였다는 사실을 확인할 수 있었습니다.

-------------------------------------------------------------------------------------------------------------------------------
<b> Q1-2. COVID19에 대응하는 정부 정책은 지하철 이용량에 영향을 주었을까?</b> 

COVID19에 대응하는 정부 정책은 지하철 이용량에 유의미한 영향을 준 것으로 나타났습니다. 분석을 위해 앞서 준비한 데이터에 더해, DS4C팀 COVID-19 데이터 중 Policy에 기록된 정부 정책 타임라인을 참조하였습니다.



```python
policy = pd.read_csv("data/covid/COVID_19 현황/policy.csv")
relevant_policy = policy[policy['start_date'] >= '2020-02-07']
relevant_policy[relevant_policy["gov_policy"].str.contains("Social Distancing")]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>policy_id</th>
      <th>country</th>
      <th>type</th>
      <th>gov_policy</th>
      <th>detail</th>
      <th>start_date</th>
      <th>end_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28</th>
      <td>29</td>
      <td>Korea</td>
      <td>Social</td>
      <td>Social Distancing Campaign</td>
      <td>Strong</td>
      <td>2020-02-29</td>
      <td>2020-03-21</td>
    </tr>
    <tr>
      <th>29</th>
      <td>30</td>
      <td>Korea</td>
      <td>Social</td>
      <td>Social Distancing Campaign</td>
      <td>Strong</td>
      <td>2020-03-22</td>
      <td>2020-04-19</td>
    </tr>
    <tr>
      <th>30</th>
      <td>31</td>
      <td>Korea</td>
      <td>Social</td>
      <td>Social Distancing Campaign</td>
      <td>Weak</td>
      <td>2020-04-20</td>
      <td>2020-05-05</td>
    </tr>
    <tr>
      <th>31</th>
      <td>32</td>
      <td>Korea</td>
      <td>Social</td>
      <td>Social Distancing Campaign</td>
      <td>Weak(1st)</td>
      <td>2020-05-06</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



특히 지하철 이용량을 감소에 가장 크게 일조한 정책은 정부가 2020년 2월 29일에 발표한 “사회적 거리두기 3단계 캠페인 (Social Distancing Campaign - Strong)”였습니다. 이전부터 COVID19 확진자 속출으로 촉발된 시민들의 불안감으로 인해 지하철 사용량은 꾸준히 감소해왔으나, 위에 제작한 그래프와 비교하며 살펴보았을 때 사회적 거리두기 3단계 캠페인을 시행한 2월 29일 이후부터는 이용량이 평일에는 <b>2019년 대비 60%대, 주말에는 40%대</b>로 꾸준히 유지되는 것을 확인할 수 있었습니다.

-------------------------------------------------------------------------------------------------------------------------------
<b> Q1-3. 각 지하철 역들의 이용량은 어떻게 변화하였을까? </b> 

같은 수도권역이라고 하지만 지하철역마다 위치, 역할이 다름에 따라 COVID19의 영향이 역마다 다를 수 있습니다. 각 지하철역의 하차 비율을 시각화함으로서 그 차이를 살펴보았습니다.



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q1-3_?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q1-3_?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q1-3_?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 우측 상당의 날짜탭을 통하여 날짜를 변경하며 보실 수 있습니다.) </b>

위 시각화에서 각 점은 지하철역을 상징하며 점의 크기는 2020년 해당 역에서 하차 인원수를 나타냅니다. 점의 색깔이 파란색에 가까울수록 19년 대비 20년 하차인원이 적은 것, 빨간색에 가까울수록 19년 대비 20년 하차 인원이 많은 것을 나타냅니다. 작년과 이용량이 비슷하다면 회색 계열을 보이도록 설정하였습니다. 

2월 초 중순에는 회색 점들이 많은 반면 시간이 지날수록 전반적으로 대부분의 지하철역들이 푸른 계열을 보입니다. 이는 COVID19 확산과 사회적 거리두기 캠페인을 통해 대부분 역에서의 이용량이 감소했음을 보입니다. COVID19 확산이 사람들간의 접촉으로 일어나는 것을 고려하였을 때 이는 긍정적인 변화입니다. 

하지만 이용량이 비슷한 회색 역들도 적지 않게 보이고, 또한 간혹 빨간색을 보이는 역, 즉 19년보다 이용량이 늘어난 역들도 확인할 수 있습니다. 3월 말부터 자주 주말에 빨간색을 보이는 여의나루역과 뚝섬유원지역에 대해서는 Q4에서 구체적으로 다루도록 하겠습니다. 

------------------------------------------------------------------------------------------------------------------------------

<div style="background-color:rgba(17, 30, 108, 1); text-align:center; vertical-align: middle; padding:0.5px 0;">
    <h3><b><center style = "color: white"> 2. 이용유형별 세분화를 통한 패턴 분석 </center></b></h3>
</div>

<b> Q2-1. 각 유형별 지하철 이용자들은 “사회적 거리두기 캠페인"에 얼만큼 영향을 받았을까?</b> 

대회에서 제공한 일자별 정책 시행표를 참고하여, 정부 정책이 지하철 이용률에 미친 영향을 분석하였습니다. 그리고 또 지하철 교통카드 이용 데이터가 이용자별 유형으로 분류되어 있다는 점을 활용해, 각 정책이 각 유형에 미친 영향을 분석하였습니다.



```python
policy[policy["policy_id"].isin([4, 29, 34, 35, 36, 37, 38])]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>policy_id</th>
      <th>country</th>
      <th>type</th>
      <th>gov_policy</th>
      <th>detail</th>
      <th>start_date</th>
      <th>end_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Korea</td>
      <td>Alert</td>
      <td>Infectious Disease Alert Level</td>
      <td>Level 4 (Red)</td>
      <td>2020-02-23</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>28</th>
      <td>29</td>
      <td>Korea</td>
      <td>Social</td>
      <td>Social Distancing Campaign</td>
      <td>Strong</td>
      <td>2020-02-29</td>
      <td>2020-03-21</td>
    </tr>
    <tr>
      <th>33</th>
      <td>34</td>
      <td>Korea</td>
      <td>Education</td>
      <td>School Closure</td>
      <td>Daycare Center for Children</td>
      <td>2020-03-02</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>34</th>
      <td>35</td>
      <td>Korea</td>
      <td>Education</td>
      <td>School Opening Delay</td>
      <td>Kindergarten</td>
      <td>2020-03-02</td>
      <td>2020-04-06</td>
    </tr>
    <tr>
      <th>35</th>
      <td>36</td>
      <td>Korea</td>
      <td>Education</td>
      <td>School Opening Delay</td>
      <td>High School</td>
      <td>2020-03-02</td>
      <td>2020-04-06</td>
    </tr>
    <tr>
      <th>36</th>
      <td>37</td>
      <td>Korea</td>
      <td>Education</td>
      <td>School Opening Delay</td>
      <td>Middle School</td>
      <td>2020-03-02</td>
      <td>2020-04-06</td>
    </tr>
    <tr>
      <th>37</th>
      <td>38</td>
      <td>Korea</td>
      <td>Education</td>
      <td>School Opening Delay</td>
      <td>Elementary School</td>
      <td>2020-03-02</td>
      <td>2020-04-06</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 지하쳘 이용자 유형 
user_type = pd.read_csv('data/card/CARD_0001/DW_USER_TYPE.dat', sep='|', header=None)
user_type.columns = ["이용자 유형 코드", "이용자 유형"]
user_type.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>이용자 유형 코드</th>
      <th>이용자 유형</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>일반인</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>어린이</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>청소년</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>경로</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>장애인</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>국가유공자</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>외국인</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>기타</td>
    </tr>
  </tbody>
</table>
</div>




```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q2-1_?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q2-1_?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b>([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q2-1_?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 하단에 위치한 슬라이더를 이용하여 날짜에 따른 변화 트랜드를 살펴보실 수 있습니다.) </b>

정책 표와 유형별 그래프를 참고하여, 다음과 같은 결론을 도출할 수 있었습니다.

<b> 전체:</b> 불규칙적으로 감소하던 비율이 2월 29일 “사회적 거리두기 캠페인 3단계" 시행 이후 규칙적으로 변동하기 시작했습니다. 해당 기간 동안의 이용객들은 필수적인 이동을 위해 지하철을 이용한 것으로 판단됩니다. 대부분 평일에 비해 주말에 지하철 사용을 자제한 것으로 보아, 불필요한 외출의 빈도가 줄어든 것으로 판단됩니다.

<b> 외국인: </b>COVID19 확산, 그리고 전염병 경보 4단계 (2월 23일 발령) 에 따른 여행 제한으로 인해 10%대 이하로 감소하였습니다. 그 이후로도 이용객 비율은 오랫동안 회복되지 않았습니다.

<b> 어린이, 청소년: </b> 유치원, 초중고등학교 개학 연기 (3월 2일 발령)로 인해 이용객 수가 현저히 줄었습니다. 

-------------------------------------------------------------------------------------------------------------------------------






<b> Q2-2. 경로/청소년 이용객의 증감율은 어떤 특성을 가지고 있을까? </b>



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q2-2_?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q2-2_?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q2-2_?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 하단에 위치한 슬라이더를 이용하여 날짜에 따른 변화 트랜드를 살펴보실 수 있습니다.) </b>

위에서 발견한 특성 이외에, 경로 및 청소년 이용객 증감률에서 다음과 같은 특이점을 발견할 수 있었습니다.

<u> (1) “경로우대 교통카드"를 사용하는 이용자 수의 감소세가 “일반 교통카드"를 사용하는 이용자 수의 감소세에 비해 큰 차이가 없었다는 점입니다. </u>

위 그래프의 파란색 곡선은 “일반 교통카드" 이용자, 그리고 분홍색 곡선은 “경로우대 교통카드” 유형의 이용 증감율 나타냅니다. 그래프에서 보이다시피, “사회적 거리두기 캠페인”이 시행된 이후로 두 곡선은 평일에는 약 10%, 주말에는 그 이하의 차이를 보이고 있습니다. 

캠페인 시행 이후로도 전체 이용자 수가 줄어들긴 했지만, “경로우대 교통카드"의 발급 대상인 65세 이상 인구의 지하철 이용량은 “일반 교통카드"를 사용하는 인구의 지하철 이용량에 비해 큰 차이를 보이지 않았습니다. “일반 교통카드”를 사용하는 인구는 경제활동을 위해 대중교통 이용이 불가피한 집단이 대부분입니다. 이를 감안하였을 때, 65세 이상 인구의 이용패턴이 이 집단의 이용패턴과 비슷하다는 것은 흥미로운 발견이었습니다.

<u> (2) 두 번째 발견은 청소년의 경우 다른 이용자 유형과 달리 주말의 하차 비율이 주중보다 많은 경우가 있었다는 것입니다. </u>

주말 하차 인원 비율의 감소세를 통해 각 이용자 유형이 COVID19 에 대해 어떤 인식을 가지고 있는지를 파악할 수 있습니다. 일반적으로 평일의 교통 이용이 출, 퇴근 등의 필수적인 이동인 반면 주말의 교통 이용은 비교적 개인 목적 그리고 선택에 의한 이동이 많습니다. 

전반적으로 보았을 때 청소년을 제외한 모든 이용자 유형에서 하차 인원 비율이 평일에는 일정 수준으로 유지되는 것을 볼 수 있습니다. 그리고 주말에는 평일 대비 하차 인원 비율이 하락하는 V자 모양을 보입니다. 주중에는 불가피한 이동을 해야하기 때문에 작년 대비 50%~60% 지하철 이용량을 보이는 반면 <b>어느 정도의 선택권이 주어진 주말에는 작년 대비 불필요한 이동을 최대한 줄이려는 노력을 하고 있는 것입니다.</b> 

하지만 노란색 곡선에서 볼 수 있듯이 청소년은 작년 대비 지하철 이용량이 크게 줄어 20%, 30%대를 유지하고 있긴 하지만 주말에 오히려 주중보다 이용량이 많은, 뒤집어진 V모양을 보여준다는 것은 흥미롭습니다. 특히 4월 주말에 이런 현상이 도드라졌습니다. 이런 현상이 발생한 원인을 Q4에서 더 깊게 분석해보았습니다. 

-------------------------------------------------------------------------------------------------------------------------------

<div style="background-color:rgba(17, 30, 108, 1); text-align:center; vertical-align: middle; padding:0.5px 0;">
    <h3><b><center style = "color: white"> 3. 경로 (65세 이상 인구)의 지하철 이용유형 패턴 분석 </center></b></h3>
</div>

<b> Q3-1. COVID19가 연령층 별로 미치는 영향은 어떤 차이가 있을까? </b>

앞에서 언급한 첫 번째 특이점에 대한 분석을 진행하기 위해, 전염병 발발 시 노령인구의 이동 패턴과 COVID19로 인한 피해의 연관성을 찾았습니다. 분석을 위해 중앙방역대책본부의 연령별 확진자 수와 치명율 데이터를 참조하였습니다.



```python
x = ['0~9세','10~19세','20~29세','30~39세','40~49세','50~59세','60~69세','70~79세', '80세 이상']
x_pos = [i for i, _ in enumerate(x)]
y = [0, 0,0, 0.08, 0.16, 0.46, 1.48, 6.81, 21.23]
df = pd.DataFrame({"구분": x, "%": y})

plt.figure(figsize = (30, 10))
splot = sns.barplot(x = "구분", y = "%", data = df)
for p in splot.patches:
    splot.annotate(format(p.get_height(), '.1f'), 
                   (p.get_x() + p.get_width()/2., p.get_height()), 
                   xytext = (0, 9), 
                   fontsize = 20,
                   fontproperties=fontprop,
                   textcoords = 'offset points',
                   ha = 'center', va = 'center')
plt.title("연령별 치명률 (8월 28일 00시 기준)", fontproperties=fontprop, fontsize = 45)
plt.xlabel("구분", size=14, fontproperties=fontprop)
plt.xticks(x_pos, x, fontproperties=fontprop)
plt.ylabel("치명률 (%)", size=14, fontproperties=fontprop)
plt.show()
```


![png](/assets/images/dacon-final_78_0.png)



```python
x = ['0~9세','10~19세','20~29세','30~39세','40~49세','50~59세','60~69세','70~79세', '80세 이상']
x_pos = [i for i, _ in enumerate(x)]
y = [406, 1104, 4202, 2401, 2580, 3481, 2773, 1381, 749]
df = pd.DataFrame({"구분": x, "%": y})

plt.figure(figsize = (30, 10))
splot = sns.barplot(x = "구분",y = "%",data = df)
for p in splot.patches:
    splot.annotate(format(p.get_height(), '.1f'), 
                   (p.get_x() + p.get_width()/2., p.get_height()), 
                   xytext = (0, 9), 
                   fontsize = 20,
                   fontproperties=fontprop,
                   textcoords = 'offset points',
                   ha = 'center', va = 'center')
plt.title("확진자 연령별 현황 (8월 28일 00시 기준)", fontproperties=fontprop, fontsize = 45)
plt.xlabel("구분", size=14, fontproperties=fontprop)
plt.xticks(x_pos, x, fontproperties=fontprop)
plt.ylabel("확진자 수", size=14, fontproperties=fontprop)
plt.show()
```


![png](/assets/images/dacon-final_79_0.png)


위 그래프에서 볼 수 있다시피, 전염병에 의한 피해를 줄이기 위해서는 치명률이 높은 60대 이상 인구의 감염을 최대한으로 방지하는 것이 중요합니다. 중앙방역대책본부의 [분석](http://ncov.mohw.go.kr/bdBoardList_Real.do)에 따르면, 8월 28일 00시 기준 연령대별 확진자 비율에선 20대가 22.03%로 가장 높으나, 전염병의 치명률은 고연령대일수록 증가하는 추세를 보입니다. 따라서 성공적인 “사회적 거리두기 캠페인”은 60대 인구의 이동과 다른 연령층 인구간 접촉 빈도를 줄여, 60대 이상 인구의 발병률을 감소시킬 수 있어야 합니다. 

그러나 Q2-2에서 확인했듯이 65세 이상 인구의 지하철 이용량은 다른 특수 이용유형(청소년, 어린이 등)에 비해 큰 변동폭을 보이지 않았습니다. COVID19에 가장 취약한 노년층이 청년 및 중장년층("일반" 교통카드 이용자)과 비슷한 패턴을 보인 것입니다. 사회적 거리두기 캠페인에도 불구하고 65세 이상 인구의 이용객 수가 대폭 줄지 않았다는 점은 정부 정책의 효과가 제한적이었다는 점을 시사합니다. 

비록 전체 이용객 수가 감소하였다고 하더라도, 60대 이상 인구의 지하철 이용객 비율이 더 큰 폭으로 떨어지지 않는다면, 국민 건강을 지키기 위해 시행되는 “사회적 거리두기 캠페인"의 효과 역시 제한적일 수밖에 없습니다. 왜 이러한 현상을 보이는지 더 심층적으로 살펴보았습니다. 

-------------------------------------------------------------------------------------------------------------------------------

<b> Q3-2. “경로우대 교통카드"를 사용하는 65세 이상 인구는 어떤 사회 활동에 참여할까?</b> 

데이터 분석을 통해, “사회적 거리두기 캠페인"에도 불구하고 65세 이상 인구의 지하철 이용량은 전년 대비 18-64세 인구의 지하철 이용량에 비해 크게 줄어들지 않았다는 점을 확인하였습니다. 캠페인 시행 및 COVID19의 위험에도 불구하고 지하철을 이용하는, 혹은 이용할 수 밖에 없는 65세 이상 인구가 어떤 사회 활동에 참여하는지 확인해보았습니다.



```python
x = ['직장', '노인정, 경로당', '복지관, 노인교실','자원봉사 활동기관이나 모임', '취미활동모임', 
 '종교단체모임', '시민단체, 사회단체','기타', '직장이나 특별한 모임이 없음']
x_pos = [i for i, _ in enumerate(x)]
y = [16.9, 33.9, 14.8, 2.1, 14.0, 20.8, 1.3, 0.4, 33.8]
df = pd.DataFrame({"구분": x, "%": y})

plt.figure(figsize = (30, 10))
splot = sns.barplot(x = "구분", y = "%", data = df)
for p in splot.patches:
    splot.annotate(format(p.get_height(), '.1f'), 
                   (p.get_x() + p.get_width()/2., p.get_height()), 
                   xytext = (0, 9), 
                   fontsize = 20,
                   fontproperties=fontprop,
                   textcoords = 'offset points',
                   ha = 'center', va = 'center')
plt.title("서울시 노인 사회활동 참가 통계", fontproperties=fontprop, fontsize = 45)
plt.xlabel("구분", size=14, fontproperties=fontprop)
plt.xticks(x_pos, x, fontproperties=fontprop)
plt.ylabel("%", size=14, fontproperties=fontprop)
plt.show()
```


![png](/assets/images/dacon-final_81_0.png)


서울특별시가 2017년 공개한 [“서울시 노인 사회활동 참가 통계”](https://data.seoul.go.kr/dataList/47/S/2/datasetView.do#) 에 따르면, 약 서울시에 거주하는 65세 이상 인구 중 약 33.8%가 “직장이나 특별한 모임이 없음”이라 응답했습니다. 그에 반해 16.9%가 “직장”을 자신의 사회 활동 중 하나라고 응답하였습니다. 

그 외로는 “노인정/경로당”이 33.9%, “종교단체모임”이 20%로 나타났습니다. 중복 응답이 가능하다는 점을 고려하면, 서울에 거주하는 65세 이상 인구 중 33.8%을 제외한 66.2% 가량이 사회활동에 참여한다는 점을 확인할 수 있습니다. 경기도, 인천 등의 수도권 지역도 서울의 통계와 비교하였을 때 크게 벗어나지 않은 분포를 보일 것으로 가정하였습니다.

-------------------------------------------------------------------------------------------------------------------------------

<b> Q3-3. 왜 65세 이상 인구의 지하철 이용량이 크게 줄지 않았을까?</b> 



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q3-3_65-?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q3-3_65-?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b>([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q3-3_65-?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 하단에 위치한 슬라이더를 이용하여 날짜에 따른 변화 트랜드를 살펴보실 수 있습니다.)</b>

앞서 언급했듯이 사회적 거리두기 시행 이후 65세 이상 인구의 지하철 사용량 변화를 살펴보았을 때, 일반 이용객과 경로 이용객에 미친 COVID19로 인한 영향이 서로 유사한 패턴으로 나타난다는 것을 확인할 수 있었습니다. 65세 이상 인구가 COVID19의 취약계층임에도 불구하고 이런 결과가 나온 것입니다.

그렇다면 특정 역에서 특별히 노령 인구의 이동 패턴과 일반 인구의 이동 패턴 사이에 큰 차이가 있을까요? 이를 확인하기 위해 인천/경기/서울 지역의 역별 일반 및 경로 이용객의 증감 비율을 시각화해보았습니다.



```python
# Tableau에서 시각화하기 위한 추가 데이터 필터 (일반과 경로만)
combined = pd.read_csv('data/additional/Card_CapitalArea_Subway_combined.csv')
general = combined[combined["이용자 유형 코드"] == 1]
old = combined[combined["이용자 유형 코드"] == 4]
combined = pd.merge(general, old, 
                    how = 'inner',
                    on = ["시도 코드","정류장 ID","날짜 인덱스","시간대"],
                    suffixes=['_일반','_경로'])
combined = combined[["시간대", "정류장 ID", "시도 코드", "하차 인원_19_일반", "하차 인원_20_일반", "하차 인원_19_경로", "하차 인원_20_경로",  "요일 구분_경로"]]
combined.to_csv("data/additional/Card_CapitalArea_Subway_General_Old.csv", index = False)
```


```python
IFrame('https://public.tableau.com/shared/XS9DCCDYG?:display_count=y&:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/shared/XS9DCCDYG?:display_count=y&:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/shared/XS9DCCDYG?:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 우측 상당의 날짜탭을 통하여 날짜를 변경하며 보실 수 있습니다.) </b>

저희는 경로 인구의 지하철 이용 비율이 적게 감소한 이유를 찾기 위해, 감소비율이 비교적 적은 역들을 필터링하여 그 이유를 살펴보기로 했습니다. 먼저 지도 상으로 패턴을 찾기 위해, ( “2020년 일자별 하차인원 수” / “2019년 일자별 하차인원 수” )가 70% 이상인 역을 분류하여 시각화하였습니다. 

2019년 4월 30일과 2020년 4월 28일을 비교한 위 그래프에서 볼 수 있다시피, 일반 이용객과 경로 이용객의 감소비율은 각각 한 가지 공통점과 차이점을 가지고 있습니다. 

첫 번째는, 수도권 중심부 (서울 지역)의 지하철역 이용률의 패턴은 일반이든 경로든 비슷한 패턴을 보입니다. 지도 상에서도 볼 수 있다시피, 중심부의 색 차이는 몇몇 예외를 제외하고는 거의 유사하다는 것을 알 수 있습니다.

두 번째는, 경로 이용객들은 수도권 외곽지역에서 지하철 이용 감소율이 더 낮다는 점입니다. 위 시각화 자료에서 볼 수 있다시피, 중심부에 비해선 외곽 지역에서 더 많은 점들을 확인할 수 있었습니다. 따라서 수도권 내에서도 중심부냐 아니냐에 따라 경로 이용객들의 증감률이 차이를 보인다는 사실을 확인할 수 있었습니다. 이를 검증하기 위해 일반 이용객 감소율과 경로 이용객 감소율을 비교하여 회귀 분석을 진행하였습니다.



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q3-3__2?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q3-3__2?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q3-3__2?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. Computation이 많아 오래 걸리거나 에러가 생길 수 있습니다. 그럴 때는 페이지 새로고침 부탁드립니다.) </b>

위 그래프는 각 역별 일반 아용객 하차 인원 증감율과 경로 이용객 하차 인원 증감율을 나타낸 것입니다 (경기도 지축역의 경우 outlier라 판단되어 제외하였습니다). 흰색 점선은 각 시도별 역들을 사용해 선형 회귀선을 그린 것입니다. 회귀선에 커서를 올려놓으시면 기울기와 P-value를 확인하실 수 있습니다. 수도권 모두 회귀선 기울기의 P-value가 매우 작은 것을 확인할 수 있었고, 서울, 경기권 지하철역의 경우 경로 이용객 하차 인원의 20/19년 비율이 일반 이용객 하차 인원의 비율보다 낮아, 회귀선이 낮은 기울기를 그리고 있는 것을 확인할 수 있었습니다.

그에 반해 인천권 지하철역의 경우 서울 경기 지역에 비해 기울기가 1에 가깝게 (약 0.88) 나타난다는 것을 확인할 수 있었습니다. 따라서 인천 지역의 경로 이용객이 다른 지역의 경로 이용객보다 일반 이용객의 이용 패턴과 유사하게 움직인다는 점을 확인할 수 있었습니다. COVID19에도 불구하고 인천 지역의 경로 이용객들은 서울, 경기 지역에 비해 지하철을 비교적 꾸준히 사용한 것입니다.

다른 지역의 노령인구에 비해 인천 지역의 노령인구의 지하철 사용률이 덜 감소했다는 점은, 사회적 거리두기 캠페인에도 불구하고 치명률이 높은 노인 인구의 이동 제한이 해당 지역에서 잘 이루어지지 못했다는 점입니다.

-------------------------------------------------------------------------------------------------------------------------------

<div style="background-color:rgba(17, 30, 108, 1); text-align:center; vertical-align: middle; padding:0.5px 0;">
    <h3><b><center style = "color: white"> 4. 청소년 (13-18세 이상 인구)의 지하철 이용유형 패턴 분석 </center></b></h3>
</div>

노령인구와는 달리, 청소년 지하철 이용객은 개학 연기령 발령 이후 급격한 지하철 이용률 감소세를 보였습니다. 하지만 1-2개월 후 부터는 차츰 이용률이 증가하더니, 특히 주말에 급격한 증가세를 보였습니다.

<b> Q4-1. 청소년이 이용하는 역이 주중과 주말 어떻게 다를까?</b>  



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q4-1_?:showVizHome=no&:embed=true', width = 850, height = 700)
```





<iframe
    width="850"
    height="700"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q4-1_?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q4-1_?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다.) </b>

주말에 평일보다 청소년 하차량이 많은 이유를 분석하기 앞서 우선 청소년의 2020년 노선별로 시간대별 평균 하차량이 가장 많은 역 20개를 선택했습니다. 각종 여가 시설이 밀집하여 있는 강남역, 홍대입구역, 롯데월드몰이 위치하여 있는 잠실역, 코엑스로 대표되는 삼성역 등이 상위권에 위치하였습니다. 또한 소위 ‘대치동 학원가’라고 일컬어지는 대치역과 한티역, 그리고 노원 학원가를 대표하는 노원역 등도 상위 20개역에서 확인할 수 있었습니다. 

해당 상위 20개 역의 하차량 순위가 평일과 주말 어떻게 바뀌는지 살펴보았습니다. 이 차이를 통해 청소년의 주말 이용량이 증가한 이유를 파악할 수 있을 것이라 예상했습니다. 



```python
IFrame('https://public.tableau.com/shared/GP5P6PR4Y?:showVizHome=no&:embed=true', width = 700, height = 800)
```





<iframe
    width="700"
    height="800"
    src="https://public.tableau.com/shared/GP5P6PR4Y?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b>([링크](https://public.tableau.com/shared/GP5P6PR4Y?:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다.) </b>

청소년의 노선별 시간대별 평균 하차량을 기준으로 하여 20개의 역을 평일과 주말을 구분하여 순위를 매겼습니다. 역이 그래프 위쪽에 위치할 경우 그보다 밑에 있는 역보다 청소년의 노선별 평균 하차량이 많은 것을 의미합니다. 

평일에는 강남역이 1위에 위치하다 주말이 되면 주중에는 4위를 기록하던 홍대입구에 1위를 넘겨주는 모습을 볼 수 있습니다. 또 주목해서 볼 역은 여의나루역과 강변역입니다. 여의나루역 같은 경우 평일에는 20위에서 주말에는 3위로 급등하는 모습을 보였고 강변역도 18위에서 12위로 상승하였습니다. 이와 같이 주말 순위가 평일 순위보다 높은 역들이 여가시설이 밀잡한 서현역, 롯데월드몰로 이어지는 잠실역 등임을 살펴보았을 때 여의나루역과 강변역도 주말간 한강시민공원 방문을 목적으로 청소년들이 많이 이용한 것으로 분석하였습니다. 



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q4-1__2?:showVizHome=no&:embed=true', width = 850, height = 576)
```





<iframe
    width="850"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q4-1__2?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q4-1__2?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다. 우측 상당의 날짜탭을 통하여 날짜를 변경하며 보실 수 있습니다.) </b> 

실제로 작년 대비 청소년 하차량이 여의나루역 기준 18%, 뚝섬유원지역 기준 97% 향상한 4월 11일-12일 주말, 젊은 층의 거리두기 문제를 지적하는 기사들이 나오기도 하였습니다. 한 기사에 따르면 한강공원 인근 따릉이 대여소에는 이렇게 자전거가 한 대도 남아있지 않았을 정도로 인파가 몰렸다고 합니다. 



```python
display(Image('img/teen_article1.png', unconfined=False))
```


![png](/assets/images/dacon-final_96_0.png)



```python
display(Image('img/teen_article2.png', unconfined=False))
```


![png](/assets/images/dacon-final_97_0.png)


-------------------------------------------------------------------------------------------------------------------------------
<b> Q4-2. 주중 대비 주말 청소년의 지하철 이용량 증가가 시사하는바는 무엇일까? </b> 

한국청소년상담복지개발원의 [설문조사](https://www.kyci.or.kr/fileup/issuepaper/IssuePaper_202002.pdf)에 따르면 50% 가량의 청소년이 ‘나와 주변사람들의 감염 위험성’과 ‘마스크, 손 씻기 등 개인위생 관리’를 거리두기로 인해 힘든 점으로 뽑은 반면 무려 72%의 청소년이 거리두기로 인하여 친구를 만나지 못하게 되는 것이 COVID19 확산으로 인해 힘든 점이라고 밝혔습니다. 길어지는 방학과 원격 수업을 비추어 보았을 때 이러한 설문 결과가 나왔을 것으로 예상됩니다. 



```python
display(Image('img/teen_survey.png', unconfined=False))
```


![png](/assets/images/dacon-final_99_0.png)


즉, 다른 이용자 유형과 달리 청소년만이 유일하게 지하철 이용량이 주말에 반등하는 트렌드를 보이는 이유는 주중에 원격 수업, 학원 등의 이유로 만나지 못한 친구들을 만나기 위해 주말에 지하철 이용량이 증가한 것에 대한 반증으로 보입니다. 비록 십분 이해가 되는 현상이긴 하지만 방치만 할 수 있는 상황은 아닙니다. 

COVID19를 연구할 때 자주 언급되는 내용이 바이러스의 치명률과 전파력입니다. 치명률 측면에서 보았을 때 현재까지 한국 기준 COVID19로 인해 사망한 10대는 없습니다. 하지만 그와 반대로 10대의 COVID19 전파력이 성인만큼 강하다는 한국 중앙방역대책본부의 [조사 결과](https://wwwnc.cdc.gov/eid/article/26/10/20-1315_article)가 있습니다. 그 이유로 성인만큼 신체적으로 성장하였지만 비위생적인 습관을 계속 가지고 있다는 것을 뽑았습니다. 또한 감염 이후 학교 및 노래방, PC방 같은 밀집 시설을 통한 집단 감염의 가능성이 있기 때문에 청소년들이 한 곳에 모이는 것을 막기 위한 방책이 필요해보입니다. 

-------------------------------------------------------------------------------------------------------------------------------

<div style="background-color:rgba(17, 30, 108, 1); text-align:center; vertical-align: middle; padding:0.5px 0;">
    <h3><b><center style = "color: white"> 5. 제언: 향후 정책에 반영할 점들 </center></b></h3>
</div>

<u> <b> 경로 인구 지하철 이용 패턴의 특수성을 고려한 해결책: 수도권 외곽 지역에서 수도권 중심부를 잇는 교통편 구축 </b> </u>

본 분석에서 살펴보았듯이 생명에 치명적임에도 불구하고 65세 경로 인구는 수도권 외곽 지역에서 지하철 이용 의존도가 높은 것으로 드러났습니다. 특히 인천 지역의 경로 인구의 감소율은 일반 이용객의 감소율에 비해서도 적은 것으로 드러났습니다. 지하철을 통한 외곽지역에서의 중심부로의 인구 흐름은 밀폐, 밀집, 밀접 현상을 증가시켜, 노령 인구의 감염률을 크게 높일 것입니다. 지하철에 대한 의존도가 높은 미국의 뉴욕의 경우, 만원 지하철의 일상화로 인해 COVID19의 전파에 큰 영향을 미쳤을 것이란 보도 역시 이를 증명합니다 ([한국경제: “"하루 지하철 500만 이용 뉴욕…코로나19 진앙돼"](https://www.hankyung.com/international/article/202003246294Y).

이유는 두 가지로 압축될 수 있습니다. 첫번째로, 지하철 외의 교통 인프라의 부재입니다. 수도권 외곽 지역과 수도권 중심 지역 사이 이동(출퇴근 등)을 위해 장시간 자가용 및 대중교통을 이용하는 경우가 많습니다 ([동아일보: “교외로 이사뒤 ‘파김치 출근’ 못견뎌 U턴” 참조](https://www.donga.com/news/Society/article/all/20141124/68118959/1)) 최근에는 적자 발생으로 인천-서울 간 버스 노선이 폐지되는 경우도 있었습니다 ([이데일리: “인천~서울 M버스 2개노선 폐선…송도주민 출퇴근 불편 가중”](https://www.edaily.co.kr/news/read?newsId=03896646622456776&mediaCodeNo=257)).

특히 현업에 종사하는 노령인구의 경우 지하철과 같은 교통 수단에 크게 의존하는 경우가 많을 것이라 예상됩니다. 또한 젊은 연령층에 비해 원격근무로 대체될 수 있는 산업에 종사하는 경우가 적을 것이기에, 이 역시 인천 지역의 적은 감소율에 영향을 미쳤을 것이라 고려됩니다. 

따라서 지하철 이용인구 분산을 위해 인천-서울 간 대체 교통 수단을 마련하는 것이 바람직하다 생각됩니다. 이는 COVID19와 같은 전염병 유행 기간 동안 수도권 외곽지역 노령 인구 유입 경로를 분산시켜 밀집도를 줄이고, 감염률을 낮춰 수도권 내 지역전파의 가능성 또한 줄일 수 있을 것입니다. 특히 노령 인구와 일반 출퇴근 인구의 동선이 겹치는 7-9시, 17-19시 구간에 지하철 외에 추가적인 대체 교통 수단을 설치하는 것을 제안합니다.

<u> <b> 청소년 인구 지하철 이용 패턴의 특수성을 고려한 해결책: 다른 역으로 흩어질 수 있는 좋은 환경 만들기 </b> </u>

사회적 거리두기 캠페인의 성공의 척도 중 하나는 불필요한 외출을 얼마나 자제시켰는지의 여부입니다. 지하철 이용객 증감률과 관련하여 지난 4월 발표된 [논문](https://www.cureus.com/articles/30376-changes-in-subway-ridership-in-response-to-covid-19-in-seoul-south-korea-implications-for-social-distancing)에 따르면, 생활에 필수적인 통근보다 불필요한 외출을 위한 지하철 이용률이 캠페인 기간 동안 더욱 크게 감소했다는 것을 알 수 있습니다. 하지만 그럼에도 불구하고, 그 적은 비율의 외출 동안에도 특정 지하철역에 인구 쏠림 현상이 발생하는 점을 확인할 수 있었습니다. 

전염병 확산을 막기 위해 가장 이상적인 해결방안은 국민들에게 불필요한 외출 자제를 당부하면서도, 외출을 하더라도 한 곳으로 집중되는 것이 아니라 균등한 이동량 분배를 도모하여 인구를 분산시키는 것입니다. 하지만 그것은 이상적인 해결방안일뿐 경제, 사회적 비용이 높을뿐더러 1분 1초가 시급한 팬데믹 상황에서 빠르고 쉽게 실현 가능한 해결방안은 아닙니다. 



```python
IFrame('https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q5_?:showVizHome=no&:embed=true', width = 700, height = 576)
```





<iframe
    width="700"
    height="576"
    src="https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q5_?:showVizHome=no&:embed=true"
    frameborder="0"
    allowfullscreen
></iframe>




<b> ([링크](https://public.tableau.com/views/COVID19_Subway_User_Analysis/Q5_?:language=en&:display_count=y&:origin=viz_share_link)를 클릭하여 큰 창으로 확인하는 방법을 추천드립니다.) </b>

그렇다면 차선책은 한 곳에서 모이더라도 그 주변으로 흩어질 수 있는 좋은 환경을 만드는 것입니다. 위 그래프에서 흰색 점선은 역들의 승차량과 하차량이 1대 1인 경우를 나타내는 45도 대각선입니다. 현재 청소년의 역별 승하차 인원을 살펴보면 대부분의 역들이 흰색 점선을 따라 배치되어있는 것을 확인할 수 있으며 즉 승차량과 하차량 비율이 거의 1대 1 비율인 것을 확인할 수 있습니다. 이는 많은 청소년들이 홍대입구역, 강남역 같은 곳에서 하차한 뒤 다른 역으로 이동하지 않고 같은 역에서 다시 승차하여 귀가를 한다는 것을 의미합니다. 승차와 하차가 결국 같은 역에서 이루어지는 일만큼 승차와 하차가 둘 다 많다는 것은 그만큼 역내 인구 밀집도가 증가한다는 것을 뜻합니다. 


```python
STTN_combined = pd.read_csv('data/additional/sttn_index_full_with_address_coord.csv')
dist_matrix = [] # 역간 거리 계산 (km 단위)
for index1, row1 in STTN_combined.drop_duplicates(["Sel 역명"]).iterrows():
    current_row = [row1["Sel 역명"]]
    current_cord = (row1["lat"], row1["long"])
    for index2, row2 in STTN_combined.drop_duplicates(["Sel 역명"]).iterrows():
        compared_cord = (row2["lat"], row2["long"])
        current_row.append(geodesic(current_cord, compared_cord).km)
    dist_matrix.append(current_row)
dist_matrix = pd.DataFrame(dist_matrix, columns = ["역명"]+list(STTN_combined["Sel 역명"].unique())).set_index("역명")

min_dist = [] # 각 역별 인접역까지 최소 거리 (km 단위)
for index, row in dist_matrix.iterrows():
    min_dist.append(np.partition(row, 1)[1])
avg_min_dist = sum(min_dist)/len(min_dist) # 각 역별 인접역까지 최소 거리의 평균 (km 단위)
avg_min_dist
```




    1.1695170125030876



수도권 역들 기준 지하철역에서 인접역까지의 최소 거리는 평균 1.16km로 걷는다면 15분-20분 정도 걸리는 짧은 거리입니다. 그 길을 따라 상권을 개발하거나 볼거리를 마련하여 걷기 좋은 환경을 조성한다면 하차는 같은 역에서 하였더라도 귀가시 근처 역에서 승차하는 효과를 기대할 수 있습니다. 잉크가 번져나가듯 이렇게 인구를 분산시키면서 COVID19 같은 전염병의 접촉을 최소화할 수 있습니다. 

이와 병행하여 청소년들도 사회적 거리두기 운동에 동참할 수 있도록 건강한 청소년기 생활을 위한 여가 인프라 구축, 교육을 통한 인식 개선 등 장기적인 노력이 필요하다고 보여집니다. 

<u> <b> 마치며 </b> </u>

본 분석을 통해 교통카드 데이터만으로도 COVID19 발발 이후 지하철 이용자들의 패턴을 파악하고 어느 역에 인구 쏠림 현상이 발생할 것이라는 것을 충분히 예측할 수 있다는 것을 확인할 수 있었습니다. 그리 복잡한 분석은 아니었지만 분석과정과 도출된 결과를 통해 나와 내 주변 사람들을 지키지 위해 어떤 날에는 어떤 역들을 피해야겠다는 생각을 충분히 할 수 있었습니다.

이런 분석은 교통공학 분야에서 말하는 Advanced Traveler Information System의 기본 구조가 될 수 있습니다. 서울의 경우 5월부터 “교통빅데이터플랫폼”을 통한 밀집도 예측 데이터를 하고 있습니다. 하지만 데이터의 존재를 알고 있는 사람은 소수일뿐더러 데이터 분석 경험이 없는 대중이 이 데이터를 기반으로 어떠한 결론을 도출하기는 쉽지 않습니다. 

따라서 가장 효과적이고 빠른 해결방안은 이러한 정보와 데이터를 시민들이 직접 사용할 수 있는 환경을 만들어주는 것이라고 생각합니다. 과거 데이터를 기반으로 하여 “대중교통 예보”를 제공해야 합니다. 서울 지역 외에도 교통 빅데이터 플랫폼의 서비스를 확장해야만 합니다. 서울의 문제는 서울 지역만이 아닌 수도권 전체의 문제라는 점을 고려하여, 시-도간 협력을 강화해야만 합니다.

지하철은 국가의 동맥입니다. 한 부분을 치료해서 건강을 되찾을 수 없습니다. 오직 단기간의 호전만을 가능케 할 뿐입니다. 수도권이라는 우리 몸의 일부분을 치료하기 위해서는 신체 전반에 대한 종합적인 진단이 필요할 것입니다.

------------------------------------------------------------------------------------------------------------------------------

본 저작물의 저작권은 Apache License v2.0을 따릅니다
