
# LLM-assisted Clinical Meta-analysis Pipeline (PubMed + LLM + Meta-analysis)

임상 질문을 입력하면 PubMed에서 관련 논문을 검색하고, 연구 데이터를 추출하여 메타분석 결과를 생성하는 AI 기반 evidence synthesis 시스템입니다.

이 프로젝트의 목표는 다음 과정을 자동화하는 것입니다.

1. 문헌 검색 (literature retrieval)
2. 연구 데이터 추출 (study data extraction)
3. 메타분석 수행 (meta-analysis)
4. 근거 기반 결과 요약 (evidence synthesis)

---

# Motivation

임상 연구에서 새로운 질문에 대한 근거를 찾기 위해서는 보통 다음과 같은 과정이 필요합니다.

1. PubMed에서 관련 논문 검색
2. 연구 설계 및 데이터 확인
3. 효과 크기 계산
4. 메타분석 수행
5. 결과 해석

이 프로젝트는 LLM을 활용하여 문헌 검색과 데이터 추출을 자동화하고,
통계적 메타분석을 통해 임상 근거를 요약하는 시스템을 구축하는 것을 목표로 합니다.

---

# Project Goal

사용자가 임상 질문을 입력하면 시스템은 다음 단계를 수행합니다.

1. PubMed에서 관련 논문 검색
2. 논문 metadata 및 abstract 수집
3. 연구 데이터 자동 추출
4. 효과 크기 계산
5. 메타분석 수행
6. 결과 요약 및 시각화

---

# Example Query

Example clinical question

```
Do GLP-1 receptor agonists reduce cardiovascular events in patients with type 2 diabetes?
```

Expected output

- 관련 논문 목록
- 연구별 효과 크기
- pooled effect size
- forest plot
- 결과 요약

---

# System Architecture

```
Clinical Question
        ↓
PubMed Retrieval
        ↓
Paper Collection
        ↓
LLM Data Extraction
        ↓
Meta-analysis Engine
        ↓
Evidence Summary
```

---

# Pipeline

## 1. Literature Retrieval

PubMed API를 사용해 관련 논문을 검색합니다.

수집 정보

- PMID
- Title
- Abstract
- Journal
- Publication Year

---

## 2. Paper Processing

논문 데이터를 분석 가능한 형태로 저장합니다.

예시 데이터 구조

```json
{
  "pmid": "12345678",
  "title": "Example study",
  "abstract": "...",
  "journal": "Journal Name",
  "year": 2022
}
```

---

## 3. Data Extraction (LLM)

LLM을 사용해 논문에서 연구 데이터를 추출합니다.

추출 대상

- sample size
- treatment group size
- control group size
- number of events
- outcome measure

예시 출력

```json
{
  "study": "Example RCT",
  "treatment_n": 120,
  "control_n": 115,
  "treatment_events": 20,
  "control_events": 35
}
```

---

## 4. Meta-analysis

추출된 데이터를 기반으로 메타분석을 수행합니다.

가능한 분석

- Risk Ratio
- Odds Ratio
- Standardized Mean Difference

통계 모델

- Fixed effects model
- Random effects model

사용 라이브러리

- statsmodels
- scipy
- pandas

---

## 5. Result Visualization

메타분석 결과를 시각화합니다.

예

- forest plot
- funnel plot

---

# Tech Stack

Language

```
Python
```

LLM

```
OpenAI API
```

Data Source

```
PubMed
```

Vector Search (optional)

```
Chroma
Qdrant
```

Statistics

```
statsmodels
scipy
pandas
```

API

```
FastAPI
```

Visualization

```
matplotlib
seaborn
```

---

# Project Structure

```
clinical-meta-llm/

data/
  raw/
  processed/

src/

  ingestion/
    pubmed_client.py

  retrieval/
    search.py

  extraction/
    llm_extractor.py

  analysis/
    meta_analysis.py

  api/
    app.py

scripts/
  ingest_pubmed.py
  run_meta_analysis.py

tests/
```

---

# Initial MVP Scope

초기 MVP 기능

- PubMed 논문 검색
- abstract 수집
- 연구 데이터 자동 추출
- Risk Ratio 기반 메타분석
- forest plot 생성

---

# Future Work

향후 확장 기능

- full-text 논문 분석
- study quality assessment
- publication bias detection
- hybrid retrieval (BM25 + vector search)
- 자동 systematic review 생성

---

# First Milestone

초기 단계 목표

1. PubMed API 연결
2. 논문 100개 수집
3. JSON 데이터 저장
4. 기본 retrieval 테스트