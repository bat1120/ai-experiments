# AI 통합 기능 실습 프로젝트

컴퓨터 비전 · LLM · OCR 등 다양한 AI 기능을 직접 구현하고, 이를 하나의 애플리케이션으로 통합한 학습 프로젝트입니다.
각 기능을 독립 모듈로 구현한 뒤, **AI 인터랙티브 코치(홈트레이닝)** 앱과 **모바일 챗봇** 앱으로 통합했습니다.

---

## 주요 기능

### 🏃 컴퓨터 비전
- **자세 추정 / 자세 모니터링** — MediaPipe Pose Landmarker · YOLOv8-pose 기반 실시간 자세 분석 및 교정 알림 (`posture_monitor.py`, `posture_logic.py`, `test_pose_estimation.py`)
- **이미지 분류** — 동물·음식·식물 카테고리 분류 + 정확도 자동 평가 (`image_classifier.py`, `test_classifier_accuracy.py`)
- **객체 탐지** — YOLOv8 기반 객체 탐지 (`object_detector.py`)
- **얼굴 인식** — facenet-pytorch 기반 얼굴 비교/인식 (`test_face_recognition.py`)

### 💬 LLM
- **챗봇** — 대화형 AI 어시스턴트 (`chat_app.py`, `llm_main.py`)
- **이메일 자동 작성/재작성** — Gemini 기반 이메일 톤 변환 (`llm_email_main.py`, `llm_email_rewriter.py`)
- **로컬 LLM 연동** — Ollama 기반 온디바이스 추론 실험 (`ollama_test.py`)
- **Gemini API 래퍼** — 공통 LLM 호출 모듈 (`gemini_ai.py`)

### 🔤 OCR
- **이미지 텍스트 추출 + 번역** — EasyOCR 기반 한글/영문 인식 (`test_ocr.py`)

### 📱 애플리케이션
- **AI 인터랙티브 코치** — 자세·얼굴·OCR을 통합한 Gradio 웹 앱 (`app.py`, `static/`, `templates/`)
- **모바일 챗봇** — KivyMD 기반 앱, GitHub Actions로 **Android APK 자동 빌드** (`main.py`, `.github/workflows/android.yml`)

---

## 기술 스택

| 분야 | 사용 기술 |
|------|-----------|
| 언어 | Python |
| 컴퓨터 비전 | PyTorch, OpenCV, MediaPipe, Ultralytics(YOLOv8), facenet-pytorch |
| LLM | Google Gemini, Ollama, Transformers |
| OCR | EasyOCR |
| 앱 / UI | Gradio, FastAPI, KivyMD |
| 빌드 | GitHub Actions (Buildozer / Android) |

---

## 실행 방법

### 1. 환경 설정
```bash
# 패키지 설치
pip install -r requirements.txt

# 환경 변수 설정 (.env)
echo "GEMINI_API_KEY=your_api_key_here" > .env
```

### 2. 모델 가중치 (최초 1회)
용량이 큰 모델 가중치는 저장소에 포함되지 않습니다. 아래는 실행 시 자동 다운로드되거나 별도 준비가 필요합니다.
- `yolov8n-pose.pt` — Ultralytics 실행 시 자동 다운로드
- `pose_landmarker_lite.task` — [MediaPipe 모델 페이지](https://developers.google.com/mediapipe/solutions/vision/pose_landmarker)에서 다운로드

### 3. 실행
```bash
# 통합 AI 코치 (웹)
python app.py

# 모바일 챗봇 (데스크톱 테스트)
python main.py

# 개별 기능 테스트
python test_pose_estimation.py
python test_ocr.py
python test_classifier_accuracy.py   # test_images/ 데이터셋으로 분류 정확도 평가
```

---

## 디렉토리 구조

```
.
├── app.py                    # 통합 AI 코치 (Gradio)
├── main.py                   # 모바일 챗봇 (KivyMD)
├── posture_monitor.py        # 실시간 자세 모니터링
├── image_classifier.py       # 이미지 분류
├── object_detector.py        # 객체 탐지 (YOLO)
├── gemini_ai.py              # Gemini API 래퍼
├── llm_*.py                  # LLM 기능 (챗봇 / 이메일)
├── test_*.py                 # 기능별 테스트
├── static/, templates/       # 웹 UI
├── test_images/              # 분류 정확도 평가용 데이터셋
└── .github/workflows/        # Android APK 빌드
```

> 다양한 AI 분야를 폭넓게 실습하며 익힌 개인 프로젝트입니다.
