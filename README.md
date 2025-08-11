# 🎬 영화 리뷰 감성 분석 프로젝트
---

## 📌 프로젝트 개요
영화 리뷰 데이터를 분석하여 **긍정**, **부정**, **중립**으로 감성을 분류하고, 그 결과를 그래프로 시각화하여 알기 쉽게 보여주는 시스템입니다.  
추가적으로 **워드클라우드**를 통해 주요 키워드의 중요도를 시각적으로 표현했습니다.

- **프로젝트 기간**: 2020.04 ~ 2020.06  
- **사용 기술**: Python, Keras, HTML, Crawling  
- **개발 환경**: Jupyter Notebook  

---

## 📂 주요 기능

### 1. 데이터 전처리
- **데이터 정제**: NULL, 공백, 영어 제거
- **불용어 제거**: 감성 분석에 불필요한 단어 제거
- **토큰화**: `Okt.morphs`를 사용하여 문장을 형태소 단위로 나눔

### 2. 감성 분석 모델 (LSTM)
- **활성 함수**: `Softmax` → 출력값을 확률로 변환
- **로스 함수**: `Categorical Crossentropy` → 분류 모델 최적화
- **옵티마이저**: `RMSprop` → 학습 속도와 안정성 향상

### 3. 웹 크롤링
- 네이버 영화 리뷰 페이지 전체 크롤링
- HTML Parser를 이용하여 리뷰 텍스트 부분만 추출

### 4. 워드클라우드
- 리뷰 데이터 전용 **불용어 사전** 구축
- 가중치를 부여하여 많이 언급된 단어의 가시성 강화

---

## 🖼 프로젝트 구조
```mermaid
flowchart TD
    %% 데이터 전처리
    CrawlingText["Crawling Text Data"] --> Okt[okt.morphs]
    TextData["Text Data"] --> Okt
    Okt --> Tokenizer["tokenizer.fit_on_texts"]
    Tokenizer --> ReviewData["Review Data (Train Data)"]

    %% 모델 학습
    ReviewData --> LSTMModel["LSTM Model"]
    CrawlingTestData["Crawling Data"] --> TrainedLSTM["학습된 LSTM Model"]
    LSTMModel -->|Model Training| TrainedLSTM
    TrainedLSTM -->|긍정/부정/중립 비율 시각화| CountWordCloud["Count, WordCloud"]

    %% 정확도 체크
    LSTMModel --> Accuracy["정확도 체크"]
   

    %% 시각화
    HTML[HTML]
    CountWordCloud -->|data visualization| HTML


```
```mermaid
flowchart TD
    %% LSTM 구조
    subgraph LSTM_Architecture[ LSTM Model 구조 ]
        Input[input] --> Embedding[Embedding]
        Embedding --> lstm[lstm]
        lstm --> Linear[Linear]
        Linear --> softmax[softmax]
        softmax --> Output[output]
    end
```

---

## 📈 학습 결과

- **train_loss** / **val_loss** 변화
- **train_acc** / **val_acc** 변화

---
## 📊 시각화 결과
<img width="656" height="817" alt="portfolio-details-3-1" src="https://github.com/user-attachments/assets/5c635370-fe81-4c85-91bb-22491e1ce125" />

