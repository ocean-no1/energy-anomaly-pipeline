# energy-anomaly-pipeline

이란 리스크로 유가가 급등하면 산업단지 에너지 비용도 폭증한다. 에너지 사용량 + WTI 유가 + 기상 데이터를 통합 분석해서 비용 이상을 조기에 감지하는 파이프라인

## 해결하는 문제

> 제조 현장에서 에너지 비용이 갑자기 올랐을 때
> "유가 때문인지, 설비 이상인지, 계절 요인인지" 구분할 수 없는 문제

## Stack

`Python` `pandas` `DuckDB` `Isolation Forest` `scikit-learn` `Streamlit` `GitHub Actions`

## Pipeline

```
data.go.kr API ──┐
EIA API (WTI) ───┤──> pandas 전처리 ──> DuckDB ──> Isolation Forest ──> Streamlit
기상청 API ──────┘
```

## Data Sources (전부 무료)

| 데이터 | 출처 | Phase |
|--------|------|-------|
| 산업단지 에너지 사용량 | 공공데이터포털 | 1 |
| WTI/Brent 유가 | EIA API (미국 에너지청) | 2 |
| 기상 관측 데이터 | 기상청 API | 2 |

## Structure

- `src/collect.py` — 다중 API 데이터 수집
- `src/transform.py` — 전처리 + 피처 엔지니어링
- `src/detect.py` — Isolation Forest 이상탐지
- `dashboard/app.py` — Streamlit 대시보드
- `.github/workflows/` — GitHub Actions 자동 수집

## Roadmap

| Phase | 내용 | 상태 |
|-------|------|------|
| 1 | 에너지 사용량 수집 + EDA + 기본 이상탐지 | 예정 |
| 2 | WTI 유가 + 기상 데이터 추가 (상관분석) | 예정 |
| 3 | Streamlit 대시보드 배포 | 예정 |
| 4 | GitHub Actions 자동화 | 예정 |

## How to Run

```bash
pip install -r requirements.txt
python src/collect.py
python src/detect.py
streamlit run dashboard/app.py
```
