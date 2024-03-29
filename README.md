konne: Korean Nested Named Entity Corpus

# 한국어 중첩 개체명 말뭉치

한국어 중첩 개체명 말뭉치 `konne`는 한국어 텍스트에 
개체명(`PS` 인물, `OG` 조직, `LC` 장소), 수량 및 시간 표현
(`QT` 수량, `TI` 시간, `DT` 날짜), 

백과사전적 대상(`EV` 사건, `AF` 인공물, `PT` 식물, `AM` 동물, `MT` 물질),
문명(`CV`) 개념(예술, 의복, 문화, 음료, 음식, 언어, 직업, 직위, 운동, 민족, 등)과
기타 용어(`TR` 이론, `FD` 학문분야, `TM` 용어).




This repository present the Korean Nested Named Entity (konne) corpus of named
entities (`PS` person, `OG` organization, `LC` location), quantity and time
expressions (`QT` quantity, `TI` time, `DT` date), and other encyclopedic
objects (`EV` events, `AF` artifacts, `PT` plants, `AM` animals, `MT` material
names), civilization (`CV`) concepts (art, building, clothing, culture, drink,
food, language, occupation, postion, sports, tribe, etc) and terminologies
(`TR` theory, `FD` field, `TM` terminology).




KLUE Benchmark의 개체명 주석 말뭉치 중 공개된
전체 원시 문장에서 개체명의 중첩 구조를 분석하고 150개 세분류 개체명 표지를 부착한
말뭉치이다.

* [개요](#개요)
  * [규모](#규모)
  * [원천 자료](#원천-자료)
  * [주석 도구와 말뭉치 파일 형식](#주석-도구와-말뭉치-파일-형식)
  * [태그셋과 가이드라인](#태그셋과-가이드라인)
* [통계](#통계)
* [참고문헌](#참고문헌)


## 개요

### 규모 

문장의 개수로 본 말뭉치의 규모는 다음과 같다.

| source   | train |  dev | total |
|---------:|------:|-----:|------:|
| wikitree | 11435 | 2534 | 13969 |
| nsmc     |  9573 | 2466 | 12039 |
| total    | 21008 | 5000 | 26008 |

### 원천 자료

원시 문장은 KLUE의 개체명 주석 말뭉치와 동일하다.
다음 저장소에서 KLUE benchmark v1.1의 원본 데이터를 확인할 수 있다.
개체명 말뭉치는 dev와 train 2개의 tsv 파일로 제공되고 있다.

- <https://github.com/KLUE-benchmark/KLUE>
- `klue-ner-v1.1_dev.tsv`
- `klue-ner-v1.1_train.tsv`

구축 과정에서 KLUE NER v1.1에 존재하는 형식 오류 및 원문 오류들을 다수
수정하였다. 수정된 결과물은 다음 저장소에서 확인할 수 있다.

- <https://github.com/korean-named-entity/KLUE/tree/ner-fix>

이렇게 수정된 KLUE 개체명 말뭉치의 원시 문장에 150개 세분류 개체명 표지를
부착하여 한국어 세분류 개체명 주석 말뭉치 `konec`을 구축하였다. 다음 링크에
공개되어 있다.

- <https://github.com/korean-named-entity/konec>

이를 바탕으로 중첩 구조를 주석하여 `konne`를 구축하였다.

### 주석 도구와 말뭉치 파일 형식

중첩 개체명 주석을 위하여 doccano를 이용하였다.

- <https://github.com/doccano/doccano>

말뭉치 파일 형식은 doccano에서 제공하는 것과 동일한 JSONL을 이용하였다.
한 행에 한 문장에 관한 정보를 제공하고 있으며 `text`이 원시 문장 형태,
`label`에 개체명 표지의 정보를 `[begin, end, label]`의 배열로 제공한다.
예시하면 다음과 같다.

```jsonl
{"id": 20488, "klue_id": "klue-ner-v1_train_20487_wikitree", "text": "남편은 '정보 비대칭 이론'의 창시자로 불리는 2001년 노벨경제학상 수상자 조지 애커로프 교수다.", "label": [[0, 2, "CV_RELATION"], [5, 14, "TR_SCIENCE"], [26, 31, "DT_YEAR"], [26, 38, "CV_PRIZE"], [26, 42, "CV_POSITION"], [26, 53, "PS_NAME"], [32, 34, "PS_NAME"], [32, 38, "CV_PRIZE"], [34, 37, "FD_SOCIAL_SCIENCE"], [39, 42, "CV_POSITION"], [43, 50, "PS_NAME"], [43, 53, "PS_NAME"], [51, 53, "CV_OCCUPATION"]]}
```
 
동일한 내용을 국립국어원 개체명 말뭉치 JSON 스키마를 준수하는 형식으로
변환한 파일도 함께 배포한다. 
  
### 태그셋과 가이드라인

국립국어원의 150개 세부분류 개체명 태그셋과 지침을 기준으로 주석하였다.
태그셋은 다음 파일에서 확인할 수 있다.

- [NIKL_NE_2021_TAGSET_150.tsv](docs/tagset/NIKL_NE_2021_TAGSET_150.tsv)
- [NIKL_NE_2021_TAGSET_150.json](docs/tagset/NIKL_NE_2021_TAGSET_150.json)

주석 작업 지침은 다음에서 확인할 수 있다.

- [한국어 중첩 개체명 말뭉치 작업자 지침](https://docs.google.com/document/d/1eAbxf7fNvjv9FkwC8-jMkOgIBEERmMGw)

태그셋 및 지침과 관련한 정보는 다음 문서에서 확인할 수 있다.

- 한국전자통신연구원(ETRI)의 '세부분류 개체명 가이드라인 2018'(2018. 12)를 기본으로 하여 국립국어원에서 수정한
- 2020년 개체명 분석 말뭉치 구축 지침 ver 1.6
  - 국립국어원 > 자료 > 연구조사자료 > 연구보고서 > [2020년 개체명 말뭉치 연구분석](https://www.korean.go.kr/front/reportData/reportDataView.do?mn_id=207&report_seq=1050&pageIndex=1)
- 2021년 개체명 분석 말뭉치 구축 지침 ver 2.1
  - 국립국어원 > 자료 > 연구조사자료 > 연구보고서 > [2021년 개체명 분석 및 개체 연결 말뭉치 연구 분석](https://www.korean.go.kr/front/reportData/reportDataView.do?mn_id=207&report_seq=1078)

국립국어원에서는 이 태그셋과 지침에 따라 개체명 표지를 부착한 말뭉치를 모두의
말뭉치 사이트에 공개하고 있다.

- 모두의 말뭉치: <https://corpus.korean.go.kr/>
- 국립국어원 개체명 분석 말뭉치 2020 (버전 2.0) 2022. 4. 1.
- 국립국어원 개체명 분석 말뭉치 2021 (버전 1.0) 2022. 4. 1.

## 통계

다음 파일에서 개체명 주석 통계를 확인할 수 있다.

- 고빈도 1000개 목록: [ne_form_label_freq_1000.tsv](docs/stat/ne_form_label_freq_1000.tsv)
- 전체 목록: [ne_form_label_freq.tsv](docs/stat/ne_form_label_freq.tsv)

컬럼은 다음과 같다.

- 컬럼1 (`form`): 개체명 형태
- 컬럼2 (`label`): 개체명 표지
- 컬럼3 (`len`): 개체명 형태의 길이 (글자수)
- 컬럼4 (`freq`): 개체명 빈도 (`train_freq + dev_freq`)
- 컬럼5 (`train_freq`): train 말뭉치에서 빈도
- 컬럼6 (`dev_freq`): dev 말뭉치에서 빈도
- 컬럼7 (`form`)
- 컬럼8 (`form_freq`): 개체명 형태 빈도. `form`이 동일한 항목의 `freq`의 총합
- 컬럼9 (`label`)
- 컬럼10 (`num_label`): 개체명 형태 `form`이 동일한 항목에 결합한 `label`의 종류의 수
- 컬럼11 (`label_freq`): 개체명 표지 빈도. `label`이 동일한 항목의 `freq`의 총합                   
             

## 참고문헌
        
- 정유남, 송영숙, 유현조(2023), 한국어 중첩 개체명의 말뭉치 구축 연구, 국어학 105, 309-344. <https://doi.org/10.15811/jkl.2023..105.009>
                     
```
@article{CheongSongYou2023,
  author    = {정유남 and 송영숙 and 유현조},
  title     = {한국어 중첩 개체명의 말뭉치 구축 연구},
  journal   = {국어학},
  year      = {2023},
  volume    = {105},
  pages     = {309-344},
  publisher = {국어학회},
  doi       = {10.15811/jkl.2023..105.009}
}
```





