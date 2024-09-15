# RAG를 활용한 보아즈 Slack봇 - **BOAchat** (mini_22Analysis) 
</br>

## Usage
- [ ] 세션
- [ ] 컨퍼런스
- [X] 미니프로젝트
- [ ] 스터디

<br/>

## Period
### 24.01.25 ~ 24.02.29

<br/>

## Team
<p align="center"><img src=https://github.com/BOAZ-bigdata/22_MiniProject_BOAchat/blob/main/docs/BOAchat_members.png width="350" height="150"/>
 
- 팀장: [유하린](https://github.com/halynyu)
- 팀원: [김이정](https://github.com/shashamalone), [이혜민](https://github.com/hyeminishailey), [전현지](https://github.com/HyunZ118)
<br/>

----
<br/>


## 프로젝트 소개 및 목적
 
RAG(Retrieval Augmented Generation)을 활용하여 BOAZ의 카톡방과 공지 pdf 등을 지식 원본으로 사용하고, 이를 기반으로 LLM(Language Model)을 실행하여 챗봇 형태로 구현하는 것을 목표로 하는 프로젝트입니다.

<br/>

## 프로젝트 구현 개요
### 1. RAG + Langchain
#### (1) RAG(Retrieval Augmented Generation, 검색 증강 생성)
- 검색 (Information Retrieval) + 생성 (Generation)
- 대규모 문서 집합에서 정보를 검색, 이를 요약하거나 관련 정보를 생성하는 등 다양한 **자연어 생성 작업**에 활용

<p align="center"><img src=https://github.com/BOAZ-bigdata/22_MiniProject_BOAchat/blob/main/docs/RAG%2C%20LangChain.png width="400" height="250"/>


- LLM의 응답 생성 전 외부의 지식 데이터 베이스 (knowledge source)를 참조하는 프로세스

- Vector DB
    - BOAZ 카톡방
    - 공지 pdf 파일
- 위 Vector DB를 기반으로 LLM 실행
- 장점
    - 정확성, 관련성 향상 : 문서를 기반으로 하여 할루시네이션과 같은 현상 감소
    - 유연성 증가 : Fine-tuning과 같은 전통적인 모델 학습 과정이 불필요
    - 사용자 중심 접근 : RAG는 사용자의 query와 요구사항에 초점을 맞추어, 사용자 경험을 개선하고 원하는 정보를 효과적으로 제공


#### (2) LangChain
[LangChain 공식 홈페이지](https://www.langchain.com/)
- 언어모델과 외부 도구를 연결하는 framework
- 문서를 불러오고, 임베딩하는 모든 과정에 사용

### 2. 파인콘(Pynecone)을 이용하여 Vector DB 구축
<p align="center"><img src=https://github.com/BOAZ-bigdata/22_MiniProject_BOAchat/blob/main/docs/VectorDB.png width="350" height="250"/>
- DB & Retriever
  - pineconeDB & cosine similarity retriever
- pure vectore database
- 자체 SaaS 클라우드 -> 정보를 손쉽게 추가, 삭제, 업데이트 가능

<br/>

## Dataset
<p align="center"><img src=https://github.com/BOAZ-bigdata/22_MiniProject_BOAchat/blob/main/docs/BOAchat_dataset.png width="550" height="350"/>
  
- 보아즈 회칙_14 개정

- 2024-1 활동 기수 공지방
    - 친바 미션
    - MT 수요조사
    - 출결 관련 공지
    - 스터디 모집 공지
    - 회계 결산 내역
    - 컨퍼런스 공지 및 안내
    - 청강 및 병행 공지


- 22기 분석 BASE 톡방
    - 멘멘 스터디 신청
    - github 관련 공지
    - 매주차 세션 장소, 시간, 발제 주제 공지
    - 과제 제출 관련 주의사항
    - 미니프로젝트 1 공지


- 출결/과제 제출 점수 샘플 데이터 구축

<br/>

## 프로젝트 구현
1. LangChain의 document loaders를 이용해 문서 형성
2. LangChain의 textsplitter를 이용해 여러 개의 chunk로 분할
3. chunk로 분할된 text에 대해 Embedding 수행 (OpenAI embedding model 사용) -> Pynecone DB에 저장
4. 챗봇에 질문이 들어왔을 때, 유사도를 판별해 가장 가까운 대답 출력
5. LLM이 QA chain에 의해 답변 생성

<br/>

## 추가 개선 사항

### 1. Prompt Template
- 원하는 어투의 답변을 받기 위해 prompt template을 사용해봤지만, 눈에 띄는 성능을 보이지 못함
- 추후 관련성 있고 일관된 언어 기반 출력을 생성하기 위해 적절한 prompt template 개선 및 사용을 목표
  
### 2. 시각화
- Slack 봇으로 챗봇을 구성하려 하였으나 연결 오류 발생
- 이번 프로젝트에서는 챗봇 결과를 보다 직관적으로 이해할 수 있도록 Gradio를 활용해 시각화
- 추후 slack 연결 오류 해결 및 slack 봇을 통한 챗봇 구현이 최종 목표

