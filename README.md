# HESTIA_VISION — YOLOv8 기반 낙상 감지 데모

HESTIA 프로젝트의 **별도 비전 데모**입니다. YOLOv8s로 사람을 검출하고, 바운딩박스의 폭이 높이보다 커지면(누운 자세) "Fall Detected"를 표시합니다. 메인 애플리케이션(HESTIA_SW)과는 통합되어 있지 않습니다.

> **English summary** — Standalone fall-detection demo: YOLOv8s person detection on a video file, flagging a fall when the person's bounding box becomes wider than it is tall. Not integrated into the main HESTIA_SW application.

## 동작 방식 (`main.py`)
1. `cv2.VideoCapture('fall2.mp4')`로 샘플 영상 프레임 읽기 → 980×740 리사이즈
2. `YOLO('yolov8s.pt')` 추론, `classes.txt`(COCO 80 클래스)로 이름 매핑
3. 신뢰도 80% 초과 `person` 박스 표시 (cvzone)
4. `height - width < 0` 이면 `Fall Detected` 표시 (종횡비 휴리스틱)
5. `t` 키로 종료

## 설치 & 실행
```bash
pip install -r requirements.txt   # ultralytics, cvzone
python main.py
```
`yolov8s.pt`는 Ultralytics 공개 가중치입니다(파일이 없으면 ultralytics가 자동 다운로드).

## 파일
`main.py` · `classes.txt` · `fall.mp4`, `fall2.mp4`(샘플 입력 영상) · `yolov8s.pt` · `requirements.txt`

## 한계
- 종횡비만 사용하므로 카메라 각도·앉은 자세에 따라 오탐 가능, 시간축(자세 변화 속도) 미사용
- 입력이 영상 파일로 고정 — 카메라 입력·알림 연동 없음

## My role
**이승석** — 데모 코드 작성 (전체 시스템 통합 담당: HESTIA_SW 참고)
