# 🏆 2024 인하 인공지능 챌린지

<p align="center">
<img src="https://github.com/user-attachments/assets/40d5461b-5d0d-473c-827c-098e501b9a70" width="600" height="450">
</p>

1. 주제 : 한국 경제 기사 분석 및 질의응답
    
    ★ 참가자 전원에게 주제 및 예제코드 관련 기초 교육 자료 제공
    
2. 대 상 : 인하대 학부 및 대학원 재학생 팀 (팀당 2~5인)
3. 대회 기간 : '24. 7. 2(화) 오후 1시 ~ 8. 14(수) 오후 6시
4. 주관: 인공지능융합연구센터, BK 산업융합형 차세대 인공지능 혁신인재 교육연구단
5. 후원: 포티투마루(42MARU)
6. 운영: 데이콘

# 대회 안내
- [인하대 인공지능융합연구센터](https://aix.inha.ac.kr/?page_id=1282&vid=81)
- [Dacon](https://dacon.io/competitions/official/236291/overview/description)

# 대회 규칙

- 평가 산식 : F1 Score
- 평가 방식: 정량 평가(100%)
- 단일 GPU VRAM(48GB)에서 모델이 작동 가능해야함
- 이 외의 규칙 [대회 공식 홈페이지](https://dacon.io/competitions/official/236291/overview/rules) 참고

# 대회 결과

- **전체 2등** (학부생 트랙 2등)
- **최종 점수:** `0.90252` [데이콘 리더보드](https://dacon.io/competitions/official/236291/leaderboard)
- **대회 결과 공지:** [대회 결과 공지](https://aix.inha.ac.kr/?page_id=3841&vid=30)
- **기사 링크:** [대학저널 기사](https://dhnews.co.kr/news/view/1065575539326139)

# Dataset Info.
※ 데이터셋 파일은 대회 규정상 공개할 수 없습니다.
- **train.csv**  
    id : 샘플 고유 ID  
    context : 금융 및 경제 뉴스 기사 관련 정보  
    question : context 정보 기반 질문  
    answer : 질문에 대한 정답 (Target)  
    33716개 샘플
    
- **test.csv**  
    id : 샘플 고유 ID  
    context : 금융 및 경제 뉴스 기사 관련 정보  
    question : context 정보 기반 질문  
    1507개 샘플

# 코드 실행 방법

- 실행 환경: colab A100

- 모델 훈련 코드
    
    `gemma2_finetuning.ipynb` rtzr/ko-gemma-2-9b-it 모델 파인튜닝 코드
    
    `eeve_finetuning.ipynb` yanolja/EEVE-Korean-Instruct-10.8B-v1.0 모델 파인튜닝 코드
    
    `nous_finetuning.ipynb` NousResearch/Nous-Hermes-2-SOLAR-10.7B 모델 파인튜닝 코드
    
- 추론 코드
    
    `Inference.ipynb` 
    
    파인튜닝한 세 개의 모델을 이용해 답을 추론한 이후
    
    앙상블 기법으로 최종 답을 추론하고 제출용 csv파일을 생성하는 코드
    
- 실행 순서
    1. 세 개의 모델 훈련 코드를 각각 실행해 각 모델을 훈련시키고 어뎁터를 `/content` 경로에 저장
        
        (만약 다른 경로로 저장했다면 추론 코드에서 어뎁터 경로를 수정)
        
    2. 추론 코드를 처음부터 ‘3. Gemma 모델 추론’까지 실행
    3. GPU memory 사용량이 1GB 미만으로 떨어지는지 확인 후 ‘4. eeve 모델 추론'실행
    4.  ‘4. eeve 모델 추론'을 전부 실행한 이후 GPU memory 사용량이 1GB 미만으로 떨어지는지 확인 후 나머지 코드 전부 실행
    
- 실행 도중 `/content` 경로에 생기는 `eeve_submission.csv`, `gemma2_submission.csv`, `nous_submission.csv` 3개의 파일은 각 모델의 추론 파일이고
최종 제출용 파일은 '/content' 경로 아래에 생기는 ensemble_final.csv 파일
