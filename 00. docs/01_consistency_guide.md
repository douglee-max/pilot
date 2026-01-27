# Gemini Veo 제작 세부 가이드라인: 일관성 유지 및 제작 절차

Gemini Veo는 약 5~15초 분량의 클립 단위로 생성되므로, 2~3분 분량의 완성도 있는 영상을 만들기 위해서는 **'분리 제작 후 통합(Decoupled Production)'** 전략이 필수적입니다. 본 가이드는 클립 간 이질감을 최소화하기 위한 구체적인 절차를 정의합니다.

---

## 1. 캐릭터 일관성 유지 (Character Consistency)

가장 어려운 부분인 '동일 인물 유지'를 위해 다음 3단계 절차를 거칩니다.

### Step 1: 캐릭터 시트(Character Sheet) 생성
- 동영상 생성 전, 이미지 생성 AI(Gemini Image 등)를 통해 캐릭터의 정면, 측면, 뒷면이 담긴 **Reference Image**를 먼저 만듭니다.
- **캐릭터 이름 부여**: 프롬프트 안에 고유한 이름을 부여하거나, 매우 구체적인 특징을 조합합니다.
    - *Bad*: "A young businessman" (매번 얼굴이 바뀜)
    - *Good*: "A 30-year-old Korean male architect, wearing distinct **matte-black thick-rimmed glasses**, a **cobalt blue linen blazer**, and a **silver smartwatch with a leather band**."

### Step 2: 캐릭터 앵커링 (Anchoring)
- Veo의 **Image-to-Video** 기능을 활용합니다. Step 1에서 만든 고해상도 캐릭터 이미지를 첫 프레임(First Frame)으로 입력하여 AI에게 외양을 고정시키도록 명령합니다.

---

## 2. 마스터 스타일 프롬프트 (Master Style Prompt)

모든 클립의 프롬프트 뒷부분에 동일하게 붙여넣을 '시각적 환경 값'을 정의합니다.

```text
[Master Style Template]
Style: Cinematic 4k, professional color grading, soft volumetric lighting.
Film: Shot on 35mm lens, shallow depth of field, subtle film grain.
Palette: Professional blue and sophisticated gray as dominant colors.
Environment: Minimalist modern office, clean glass backgrounds.
```

- **효과**: 장면이 바뀌어도 조명과 색감, 카메라의 질감이 동일하므로 전체적으로 한 감독이 찍은 듯한 일관성을 줍니다.

---

## 3. 숏 리스트(Shot List) 기반 분절 제작 절차

2~3분 영상을 약 30~40개의 '숏(Shot)'으로 쪼개어 관리합니다.

| 숏 번호 | 시간 | 주요 내용 | 비주얼 프롬프트 핵심 | 일관성 체크 항목 |
| :--- | :--- | :--- | :--- | :--- |
| #01 | 0-10s | 도입: 서비스 명칭 등장 | [Master Style] + 오피스 전경 | 배경 색감 |
| #02 | 10-20s | 주인공 등장 (문제 제기) | [Master Style] + [Character Info] + 책상 앞 고민 | 캐릭터 의상/안경 |
| #03 | 20-30s | 아키텍처 다이어그램 분석 | [Master Style] + [Character Info] + 태블릿 조작 | 캐릭터 손/소품 |

### 델타(Delta) 관리 원칙
- 이전 숏과 다음 숏 사이의 **프롬프트 변화량(Delta)을 20% 이내**로 유지합니다. 
- 예: 숏 #01에서 사용한 배경 묘사를 숏 #02에서도 80% 이상 재사용하고 주체(캐릭터)만 추가합니다.

---

## 4. 환경 및 배경 유지 (Environmental Continuity)

- **배경 고정**: 동적이지 않은 배경(정적인 사무실, 데이터 센터 내부 등)을 먼저 영상으로 생성한 뒤, 그 위에 캐릭터가 움직이게 하는 방식(가능한 경우 Masking 활용)을 고려합니다.
- **조명 고정**: "Key light from the left, cool shadows" 와 같이 조명 위치를 명시하여 숏마다 그림자 방향이 바뀌는 것을 방지합니다.

---

## 5. 제작 및 통합 절차 (Workflow)

1.  **Prep**: 캐릭터 이미지 생성 및 마스터 프롬프트 확정.
2.  **Pilot**: 가장 중요한 3개 숏(#01, #02, #03)을 먼저 생성하여 이질감 테스트.
3.  **Batch Production**: 확정된 프롬프트 체계로 전체 숏 생성.
4.  **Assembly**: 영상 편집 툴(Premiere, Final Cut 등)에서 클립 배치.
5.  **Smoothing**: 클립 간 전환 시 **디졸브(Dissolve)**나 **매치 컷(Match Cut)**을 사용하여 시각적 튐 현상을 완화.

---
> [!IMPORTANT]
> **Gemini Veo의 특성상 완벽한 100% 일관성은 어렵습니다.** 
> 따라서 의상 컬러나 액세서리(안경, 시계)처럼 시각적으로 눈에 띄는 요소를 '고정 장치'로 활용하는 것이 핵심입니다.
