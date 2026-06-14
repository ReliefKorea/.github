# Relief Korea

> Disaster Response · Relief Connection · Trusted Action

도움이 필요한 순간, 마음이 길을 잃지 않도록

지금 한국에서 발생한 재난을 한눈에 확인하고, 공식 정보와 검증 가능한 지원 방법을 따라 가장 필요한 곳에 빠르게 마음을 전하세요.

**Relief Korea**는 재난 소식이 실제 도움으로 이어지도록 연결하는 **재난 대응 시각화 및 구호 연결 플랫폼**입니다.


---

## Table of Contents

* [Overview](#overview)
* [Core Features](#core-features)
* [System Architecture](#system-architecture)
* [Tech Stack](#tech-stack)
* [Data Sources](#data-sources)
* [AI Recommendation Flow](#ai-recommendation-flow)
* [Project Structure](#project-structure)
* [Getting Started](#getting-started)
* [Team](#team)

---

## Overview

재난 뉴스는 많지만, 후원으로 이어지는 길은 여전히 끊겨 있습니다.

사용자는 뉴스를 본 뒤 직접 구호 단체를 검색해야 하고, 그 단체가 후원금을 제대로 사용하는지도 따로 확인해야 합니다.

누군가의 재난이 뉴스로만 지나가지 않도록, Relief Korea는 신뢰할 수 있는 정보와 따뜻한 행동을 연결합니다.


---

## Core Features

### 1. Live Disaster Map

현재 재난 이벤트를 지도 기반으로 탐색할 수 있는 인터페이스입니다.

**주요 기능**

* 재난 위치 기반 지도 시각화
* 클러스터링된 재난 마커
* 재난 유형별 필터링
* 심각도별 필터링
* 지역별 필터링
* 최신 업데이트 기준 정렬
* 재난 이벤트 카드 제공
* 공식 근거 및 구호 행동 링크 연결

---

### 2. Disaster Detail Page

각 재난 이벤트에 대해 사용자가 행동 전 확인해야 할 정보를 한 화면에 제공합니다.

**제공 정보**

* 재난 요약
* 발생 위치
* 심각도
* 공식 경보 및 업데이트
* 관련 뉴스 기사
* 추천 구호 단체
* 외부 기부 또는 봉사 링크

---

### 3. Evidence-Based Relief Recommendations

Relief Korea는 AI-assisted retrieval 기반 추천 흐름을 통해 특정 구호 단체가 왜 해당 재난과 관련 있는지 설명합니다.

추천은 다음 요소를 함께 고려합니다.

* 재난 유형
* 재난 발생 지역
* 구호 단체의 활동 분야
* 공식 단체 자료
* 관련 뉴스 근거
* 기부금 사용 가능성
* 신뢰 신호
* 출처 링크

기부 버튼은 맥락, 근거, 추천 이유가 제시된 이후에 노출됩니다.

---

## System Architecture

```text
Public Disaster Data
        ↓
Backend Normalization + SQLite
        ↓
Express REST API
        ↓
React Disaster Map / Detail UI
        ↓
OpenAI RAG Recommendation Layer
        ↓
Relief Organization Evidence + Action Links
```

---

## Tech Stack

### Frontend

* TypeScript
* React 19
* Vite
* React Router
* Leaflet
* React Leaflet
* Marker Cluster
* React Globe.gl
* Custom CSS / In-house Design System
* OpenStreetMap / CARTO Map Tiles

### Backend

* Node.js
* Express
* SQLite
* Axios
* Fetch API
* REST API
* JWT Administrator Authentication
* bcrypt Password Verification

### AI / RAG

* OpenAI API
* GPT-4o-mini
* text-embedding-3-small
* SQLite-stored Embeddings
* Retrieval-Augmented Generation without a separate vector database

---

## Data Sources


* Korea Meteorological Administration weather warning data
* Ministry of the Interior and Safety disaster text messages
* Korea Forest Service wildfire-related data
* ReliefWeb disaster and report data
* Naver News search results
* Verified relief organization materials


---

## AI Recommendation Flow


```text
Disaster Event
   ↓
Query Construction
   ↓
Embedding Search
   ↓
Relevant Organization Evidence
   ↓
RAG-based Recommendation
   ↓
Rationale + Trust Signals + Action Links
```

### Recommendation Output

AI 추천 결과는 다음 정보를 포함합니다.

* 추천 구호 단체명
* 추천 이유
* 재난 유형과의 관련성
* 지역 또는 활동 영역과의 관련성
* 근거 자료 요약
* 신뢰 가능한 출처 링크
* 기부 또는 봉사 행동 링크

---

## Project Structure

```text
relief-korea/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── styles/
│   │   └── data/
│   └── package.json
│
├── backend/
│   ├── src/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── db/
│   │   ├── auth/
│   │   └── rag/
│   └── package.json
│
└── README.md
```

---

## Getting Started

### Prerequisites

* Node.js
* npm
* SQLite
* OpenAI API Key

---

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

---

### Backend Setup

```bash
cd backend
npm install
npm run dev
```

---

### Environment Variables

Backend 환경에서 다음 변수가 필요할 수 있습니다.

```env
OPENAI_API_KEY=your_openai_api_key
JWT_SECRET=your_jwt_secret
```

---

## Key Design Principles

### Trust Before Action

Relief Korea는 사용자가 기부나 봉사 링크를 클릭하기 전에 충분한 맥락과 근거를 확인할 수 있도록 설계되었습니다.

### Source-Based Explanation

AI 추천 결과는 공식 자료, 뉴스, 구호 단체 자료 등 출처 기반 근거를 함께 제공합니다.

### Resilient Demonstration

외부 API나 데이터 소스가 불완전한 상황에서도 mock data와 정규화된 backend records를 통해 안정적인 시연이 가능합니다.

### Human-Centered Disaster UX

재난 상황에서는 정보의 양보다 명확성과 신뢰성이 중요합니다. Relief Korea는 사용자가 빠르게 이해하고, 검증하고, 행동할 수 있는 흐름을 우선합니다.

---

## Team

| Role        | Name         | Responsibility |
| ----------- | ------------ | -------------- |
| Team Leader | Sujin Yoon   | PM, AI         |
| Member      | Yeonseo Nam  | Frontend       |
| Member      | Junseo Jeong | Backend        |

---

## Project Goal

Relief Korea의 목표는 사용자가 신뢰할 수 있는 근거를 바탕으로 재난을 이해하고, 공감에서 행동으로 이어지는 회복 지원에 참여할 수 있도록 돕는 것입니다.

누군가의 재난이 뉴스로만 지나가지 않도록, Relief Korea는 신뢰할 수 있는 정보와 따뜻한 행동을 연결합니다.
