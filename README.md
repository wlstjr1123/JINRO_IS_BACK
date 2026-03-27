## AI 기반 진로 상담 지원 플랫폼 개발 - 너 내 진로가 되라
* **시연 영상은 필요하실때 연락주시면 보내드립니다**
* [문서및 가상환경](https://drive.google.com/drive/folders/1U52hYSRpNeul6byyYGkKamrlGaNVSBgt?usp=drive_link)

### 개요
* 기존 진로 상담은 학생의 주관적 응답과 상담사의 메모에 크게 의존하기 때문에, 상담 내용을 객관적으로 구조화하고 이후 판단에 활용하기 어렵다는 한계가 있습니다. 이 프로젝트는 학생의 영상 시청 반응, 설문 결과, 상담 대화처럼 서로 다른 형태의 데이터를 AI로 통합 분석해 상담 과정의 보조 도구로 활용하고자 기획 되었습니다.
* AI 모델 자체보다도 AI가 실제 상담 서비스 안에서 어떻게 입력을 받고, 어떤 형태의 결과로 정리되어 의사결정에 도움을 줄 수 있는지를 보여주는 것이 핵심 기획의도입니다.

### 프로젝트 참여도 및 기술 스택
* 개발 언어 및 프레임워크 : Python, JavaScript, FastAPI, React, Vite
* 데이터베이스 : MySQL
* 프론트엔드 및 상태관리 : React Router, Redux Toolkit, Axios
* AI 및 데이터 분석 도구 : OpenCV, MediaPipe, TensorFlow, PyTorch, scikit-learn, Whisper, Ollama, OpenAI API
* 시각화 및 문서화 도구 : Recharts, FullCalendar, html2canvas, jsPDF
* 외부 연독 API 및 서비스 : YouTube IFrame API, OpenAI API
* 협업 및 관리 도구 : GitHub, Google Drive
* 활용 장비 : 웹캠, 마이크, PC/노트북
* 서버 및 실행 환경 : FastAPI 서버, Uvicorn, GitHub 기반 형상관리 환경

### 내담자 화면 응시 3초간 확인
* 내담자가 영상 분석을 하기전 웹캠을 정면으로 응시하고있는지 판단하기 위해 미디어파이스 페이스매쉬를 활용하여 단순히 화면에 얼굴이 있는지 확인하는것을 넘어 사용자가 정확히 정면을 응시하고있는 계산하는 로직을 구현
* 코와 왼쪽과 오른쪽 끝 세점의 좌표를 구하여 정면응시 판단 코드 구현
<img width="600" height="600" alt="Image" src="https://github.com/user-attachments/assets/c046abf9-1bad-4af0-b437-2b02a7429ac9" />
<img width="600" height="600" alt="Image" src="https://github.com/user-attachments/assets/1930a173-99b7-4aa0-8d36-a1e7165c3637" />

### 흥미도 모델
* AffectNet 데이터셋을 통해 이미 수많은 이미지로 사전학습된 ResNet50 모델을 사용하여 전이학습을 수행하여 흥미도모델은 만들었다
* 이미 ResNet50 모델이 가지고있는 시각적 특징 추출 능력은 활용하되 마지막 분류기만 우리의 목적인 2개의 클래스에 맞게 수정하여 학습시간을 단축
* AffectNet이 가지고 있는 8개의 감정 라벨을 흥미있음과 흥미없음으로 이진분류로 나누어 데이터를 재정의
* 데이터의 불균형이 심하여 손실함수에 클래스 가중치를 부여하여 데이터가 적은 흥미있음 클래스에 가중치를 좀더 부여하여 흥미있는 클래스가 틀렸을 경우 모델이 더 큰 패널티를 받도록 조정
* 과적합을 방지하기위해 조기종료 기법을 도입

### DB 구조
<img width="1475" height="1263" alt="Image" src="https://github.com/user-attachments/assets/e83a35c8-abb0-46d7-8410-00f9929d4b5c" />
