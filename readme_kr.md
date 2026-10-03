<div align="center">

# Synthetic Singers

## 딥러닝 기반 가창 음성 합성 접근법에 대한 종합 리뷰

**IJCNLP-AACL 2025 · 구두 발표**

Changhao Pan, Dongyu Yao, Yu Zhang, Wenxiang Guo,<br>
Jingyu Lu, Zhiyuan Zhu, Zhou Zhao

저장대학교

[![arXiv](https://img.shields.io/badge/arXiv-2601.13910-b31b1b.svg?logo=arxiv&logoColor=white)](https://arxiv.org/abs/2601.13910v1)
[![ACL Anthology](https://img.shields.io/badge/ACL%20Anthology-IJCNLP--AACL%202025-1f6feb.svg)](https://aclanthology.org/2025.ijcnlp-long.24/)
[![GitHub Stars](https://img.shields.io/github/stars/DaViD-Pigeon/SyntheticSingers?style=social)](https://github.com/DaViD-Pigeon/SyntheticSingers)

[English](README.md) · [简体中文](readme_zh.md) · **한국어** · [日本語](readme_ja.md)

**[모델](#publicly-available-singing-voice-synthesis-models) · [데이터셋](#open-source-datasets) · [도구](#annotation-tools-for-singing-data)**

</div>

<a name="quick-start"></a>

## 🚀 빠른 안내

이 저장소는 **Synthetic Singers: A Review of Deep-Learning-based Singing Voice Synthesis Approaches**의 공식 저장소입니다. 논문은 **IJCNLP-AACL 2025에서 구두 발표**되었습니다. [ACL Anthology](https://aclanthology.org/2025.ijcnlp-long.24/) 또는 [arXiv](https://arxiv.org/abs/2601.13910v1)에서 읽을 수 있습니다.

- **과제 분류.** 고충실도 합성, 제어 가능한 합성, 가창 스타일 전이, 텍스트 기반 노래 생성을 살펴봅니다.
- **시스템 구조.** 리뷰의 도식을 통해 단계형 시스템과 종단 간 가창 합성 시스템의 차이를 이해합니다.
- **대표 모델.** 주요 연구 분야별로 모델을 탐색하고 간단한 설명과 공개 자료 링크를 확인합니다.
- **연구 자료.** 가창 데이터셋, 코퍼스 규모 통계, 정렬·전사·분리·향상 도구를 찾을 수 있습니다.

## 목차

1. [소개](#introduction)
2. [전체 구성](#overall)
3. [가창 음성 합성 과제](#tasks-of-svs)
4. [가창 음성 합성 시스템 구조](#architectures-of-svs-systems)
5. [대표 모델 및 자료](#publicly-available-singing-voice-synthesis-models)
   - [2026년 주요 연구 (1–10월)](#highlights-2026)
   - [가창 음성 합성 및 보코더](#singing-synthesis-and-vocoders)
   - [스타일 제어 및 전이](#style-control-and-transfer)
   - [노래 및 음악 생성](#song-and-music-generation)
   - [관련 음성 및 가창 모델](#related-speech-and-singing-models)
6. [자료](#resources-in-svs-models)
   - [공개 데이터셋](#open-source-datasets)
   - [주석 및 전처리 도구](#annotation-tools-for-singing-data)
7. [인용](#citation)
8. [기여 안내](#contributing)
9. [라이선스](#license)
10. [업데이트 기록](#update)

---

<a name="introduction"></a>

## 📌 소개

**Synthetic Singers**는 딥러닝 기반 가창 음성 합성의 과제, 구조, 모델, 데이터 자료를 모았습니다. 이 저장소는 [종합 리뷰 논문](https://aclanthology.org/2025.ijcnlp-long.24/)의 부속 자료로, 연구자와 실무자를 위한 읽기 안내를 제공합니다.

개요 도식은 리뷰의 구성과 기술적 관점을 보여줍니다. 자료 표는 이러한 관점을 개별 프로젝트와 연결하여 관련 시스템을 찾고 가창 데이터를 준비하는 데 도움을 줍니다.

---

<a name="overall"></a>

## 🧭 전체 구성

<div align="center">
  <img src="figure/organization.png" alt="Synthetic Singers 종합 리뷰의 전체 구성" width="90%">
  <p><em>그림 1. Synthetic Singers 종합 리뷰의 전체 구성.</em></p>
</div>

---

<a name="tasks-of-svs"></a>

## 🎯 가창 음성 합성 과제

이 리뷰는 가창 음성 합성을 네 가지 과제로 분류합니다. 하나의 시스템이 여러 과제를 지원할 수도 있습니다.

| 과제 | 주요 목표 | 주요 확인 사항 |
| --- | --- | --- |
| **고충실도 합성** | 가사와 선율에 맞는 명료하고 자연스러운 가창을 생성합니다. | 음질, 가사 명료도, 음정 정확도. |
| **제어 가능한 합성** | 합성 품질을 유지하면서 가창 속성을 조절합니다. | 음색, 스타일, 표현, 가창 기법의 제어. |
| **가창 스타일 전이** | 참조 가창의 음성 특성을 재현합니다. | 참조 오디오의 음색, 스타일, 표현 전이. |
| **텍스트 기반 노래 생성** | 텍스트 입력으로 완성된 노래를 생성합니다. | 보컬, 반주, 음악 구조의 일관성. |

<div align="center">
  <img src="figure/tasks.png" alt="가창 음성 합성 과제 개요" width="90%">
  <p><em>그림 2. 가창 음성 합성의 네 가지 대표 과제.</em></p>
</div>

---

<a name="architectures-of-svs-systems"></a>

## 🏗️ 가창 음성 합성 시스템 구조

파형 생성이 별도의 보코더에 의존하는지에 따라 두 가지 구조로 구분합니다.

| 방식 | 합성 과정 | 주요 구성 요소 |
| --- | --- | --- |
| **단계형 가창 음성 합성** | 음향 특징을 예측한 뒤 파형으로 변환합니다. | 음향 모델과 별도의 보코더. |
| **종단 간 가창 음성 합성** | 통합된 합성 시스템 안에서 파형을 생성합니다. | 조건 정보, 중간 표현, 파형 생성의 공동 모델링. |

<div align="center">
  <img src="figure/arch.png" alt="가창 음성 합성 시스템의 구조적 분류" width="90%">
  <p><em>그림 3. 단계형 및 종단 간 가창 합성 구조. 점선은 선택 구성 요소를 나타냅니다.</em></p>
</div>

---

<a name="publicly-available-singing-voice-synthesis-models"></a>

## 📚 대표 모델 및 자료

모델은 주요 연구 목적별로 분류하며 기능은 겹칠 수 있습니다. **Paper**는 논문·프리프린트, **Code**는 구현, **Model**은 가중치 또는 다운로드 안내, **Demo**는 예시를 뜻합니다. **Repo (planned)**는 공개 예정인 공식 저장소이며 코드·가중치 공개를 의미하지 않습니다. 확인된 유형의 링크만 수록하므로 링크가 없다고 미공개가 확정된 것은 아닙니다. 비공식 구현과 **Model (TTS)** 등 용도가 한정된 버전은 별도로 표시합니다.

<a name="highlights-2026"></a>

### 2026년 주요 연구 (1–10월)

**수록 범위: 2026-01-01–2026-10-03.** 이번에 추가한 12편은 악보 기반 가창 합성, 발화·가창 전환, 가사 편집, 전체 곡 생성을 다룹니다. 날짜는 논문이 처음 공개된 월이며 코드·가중치 공개일과 다를 수 있습니다. 학회 표기는 정식 논문집에 근거하며 나머지는 프리프린트 또는 기술 보고서입니다. 기존 논문의 2026년 개정판을 새 연구로 집계하지 않습니다.

| 연구 | 최초 논문 / 학회 | 연구 내용 | 자료 |
| --- | --- | --- | --- |
| HeartMuLa | 2026-01 · 프리프린트 / 기술 보고서 | 가사, 스타일 설명, 참조 오디오를 조건으로 곡을 생성하며 저프레임률 음악 코덱을 함께 제공. | [Paper](https://arxiv.org/abs/2601.10547v3) · [Code](https://github.com/HeartMuLa/heartlib) · [Model](https://huggingface.co/HeartMuLa/HeartMuLa-oss-3B-happy-new-year) |
| ACE-Step 1.5 | 2026-01 · 프리프린트 / 기술 보고서 | 언어 모델의 곡 설계와 확산 생성을 결합하며 편집과 경량 개인화를 지원. | [Paper](https://arxiv.org/abs/2602.00744v3) · [Code](https://github.com/ace-step/ACE-Step-1.5) · [Model](https://huggingface.co/ACE-Step/Ace-Step1.5) |
| SoulX-Singer | 2026-02 · 프리프린트 / 기술 보고서 | 악보 또는 멜로디를 조건으로 하는 제로샷 가창 합성. 중국어 표준어, 영어, 광둥어 지원. | [Paper](https://arxiv.org/abs/2602.07803v2) · [Code](https://github.com/Soul-AILab/SoulX-Singer) · [Model](https://huggingface.co/Soul-AILab/SoulX-Singer) |
| YingMusic-Singer / Plus | 2026-03 · Interspeech 2026 | 수동 정렬 없이 멜로디를 유지하는 가사 편집. 코드와 가중치는 후속 Plus 버전. | [Paper](https://www.isca-archive.org/interspeech_2026/hao26_interspeech.html) · [Preprint](https://arxiv.org/abs/2603.24589) · [Code](https://github.com/ASLP-lab/YingMusic-Singer-Plus) · [Model](https://huggingface.co/ASLP-lab/YingMusic-Singer-Plus) |
| UniVocal | 2026-06 · ACL 2026 | 텍스트로 제어하는 말하기·노래 전환. 공식 저장소의 코드, 가중치, SCSBench는 공개 예정 상태. | [Paper](https://aclanthology.org/2026.acl-long.1452/) · [Repo (planned)](https://github.com/QwenAudio/FunResearch/tree/main/UniVocal) · [Demo](https://project-univocal-demo.github.io/demo/) |
| UniVoice | 2026-06 · 프리프린트 / 기술 보고서 | 내용, 멜로디, 음색 조건을 분리한 음성·가창 통합 플로 매칭 프레임워크. | [Paper](https://arxiv.org/abs/2606.05852v1) |
| MeloDISinger | 2026-06 · Interspeech 2026 | 플로 매칭 인필링으로 가사를 편집하면서 멜로디, 길이, 편집하지 않은 구간을 보존. | [Paper](https://www.isca-archive.org/interspeech_2026/park26k_interspeech.html) · [Preprint](https://arxiv.org/abs/2606.30580v1) · [Demo](https://cottonlove.github.io/MeloDISinger_demo/) |
| LeVo 2 | 2026-06 · 프리프린트 / 기술 보고서 | 보컬·반주 스트림과 확산 음악 코덱을 결합한 계층적 곡 모델링. | [Paper](https://arxiv.org/abs/2606.30642v1) · [Code](https://github.com/levo-demo/LeVo) · [Model](https://huggingface.co/lglg666/SongGeneration-v2-large) |
| Qwen-Music | 2026-07 · 프리프린트 / 기술 보고서 | Melody-CoT 설계와 플로 매칭 오디오 생성을 통한 곡 생성 및 커버. | [Paper](https://arxiv.org/abs/2607.11699v3) |
| VocalRender | 2026-07 · 프리프린트 / 기술 보고서 | 가사, 음높이, 음표 길이, 템포를 입력으로 사용하는 악보 기반 자기회귀 확산 가창 합성. | [Paper](https://arxiv.org/abs/2607.27768v1) · [Code](https://github.com/pymaster17/VocalRender) · [Model](https://huggingface.co/pymaster/VocalRender) · [Data](https://huggingface.co/datasets/pymaster/CrawlSinger-OS) |
| DiffSynth-Music | 2026-09 · 프리프린트 / 기술 보고서 | ACE-Step 기반으로 오디오 조건을 이용해 비트, 보컬, 반주, 운율, 참조 음색을 제어. | [Paper](https://arxiv.org/abs/2609.12774v1) · [Code](https://github.com/modelscope/DiffSynth-Studio/tree/main/examples/diffsynth_music) · [Model](https://modelscope.cn/models/DiffSynth-Studio/DiffSynth-Music) |
| YuE2 | 2026-09 · 프리프린트 / 기술 보고서 | 편집 가능한 멜로디·코드 설계 후 전체 곡 오디오를 생성하며 제로샷 커버를 지원. | [Paper](https://arxiv.org/abs/2609.33757v1) · [Code](https://github.com/multimodal-art-projection/YuE) · [Model](https://huggingface.co/m-a-p/YuE2-3B) |

<a name="singing-synthesis-and-vocoders"></a>

### 가창 음성 합성 및 보코더

| 모델 | 주요 연구 내용 | 자료 |
| --- | --- | --- |
| DiffSinger | 얕은 확산을 활용한 가창 음성 합성. | [Paper](https://arxiv.org/abs/2105.02446) · [Code](https://github.com/MoonInTheRiver/DiffSinger) · [Model](https://github.com/MoonInTheRiver/DiffSinger/releases) |
| VISinger(비공식 구현) | 변분 추론과 적대적 학습을 결합한 종단 간 가창 합성. | [Paper](https://arxiv.org/abs/2110.08813) · [Code](https://github.com/So-Fann/VISinger) |
| VISinger 2 | 디지털 신호 처리 합성기로 개선한 종단 간 합성. | [Paper](https://arxiv.org/abs/2211.02903) · [Code](https://github.com/zhangyongmao/VISinger2) · [Model](https://drive.google.com/file/d/1MgXLQuquPT2qu1__JNF010-tg48N0hZn/view) |
| VI-SVS | VITS 기반 가창 음성 합성. | [Code](https://github.com/PlayVoice/VI-SVS) · [Model](https://github.com/PlayVoice/VI-SVS/releases/tag/0.0.3) |
| NNSVS | 신경망 기반 가창 음성 합성 연구용 라이브러리. | [Paper](https://arxiv.org/abs/2210.15987) · [Code](https://github.com/nnsvs/nnsvs) |
| CoMoSpeech | 일관성 모델을 활용한 단일 단계 음성 및 가창 합성. | [Paper](https://arxiv.org/abs/2305.06908) · [Code](https://github.com/zhenye234/CoMoSpeech) · [Model (TTS)](https://drive.google.com/drive/folders/1rkbzl9NzS_fKtMubQ7FgSdgt7v8ZuYGk) |
| HiFiSinger | 고충실도 신경망 가창 합성. 링크는 Muzic 연구 개요로 연결됩니다. | [Paper](https://arxiv.org/abs/2009.01776) · [Overview](https://github.com/microsoft/muzic) |
| HiFiSinger(비공식 구현) | HiFiSinger의 독립 구현. | [Paper](https://arxiv.org/abs/2009.01776) · [Code](https://github.com/CODEJIN/HiFiSinger) |
| ByteSing | 길이 모델링과 WaveRNN 보코더를 활용한 중국어 가창 합성. | [Paper](https://arxiv.org/abs/2004.11012) |
| WeSinger | 데이터 증강과 보조 손실을 활용한 가창 합성. | [Paper](https://arxiv.org/abs/2203.10750) · [Demo](https://zzw922cn.github.io/wesinger/) |
| SingGAN | 고충실도 가창을 위한 적대적 파형 생성. | [Paper](https://arxiv.org/abs/2110.07468) · [Demo](https://singgan.github.io/) |
| UniSinger | 모달리티 간 정보 매칭을 활용한 통합 종단 간 가창 합성. | [Paper](https://doi.org/10.1145/3581783.3612150) · [Repo (planned)](https://github.com/ViEm-ccy/UniSinger) · [Demo](https://unisinger.github.io/Samples/) |
| Learn2Sing 2.0 | 가수의 가창 데이터로 학습하여 목표 화자의 가창을 합성. | [Paper](https://arxiv.org/abs/2203.16408) · [Code](https://github.com/WelkinYang/Learn2Sing2.0) · [Demo](https://welkinyang.github.io/Learn2Sing2.0/) |
| UniSyn | 통합된 종단 간 텍스트 음성 변환 및 가창 합성. | [Paper](https://arxiv.org/abs/2212.01546) |

<a name="style-control-and-transfer"></a>

### 스타일 제어 및 전이

| 모델 | 주요 연구 내용 | 자료 |
| --- | --- | --- |
| StyleSinger | 학습 도메인 밖의 가창 음성에 대한 스타일 전이. | [Paper](https://arxiv.org/abs/2312.10741) · [Code](https://github.com/AaronZ345/StyleSinger) · [Model](https://huggingface.co/AaronZ345/StyleSinger) |
| TCSinger | 스타일 전이와 다수준 제어를 지원하는 제로샷 가창 합성. | [Paper](https://aclanthology.org/2024.emnlp-main.117/) · [Code](https://github.com/AaronZ345/TCSinger) · [Model](https://huggingface.co/AaronZ345/TCSinger) |
| TCSinger 2 | 사용자 맞춤형 다국어 제로샷 가창 합성. | [Paper](https://arxiv.org/abs/2505.14910) · [Code](https://github.com/AaronZ345/TCSinger2) |
| FreeStyler | 랩 생성. 링크된 RapBank 저장소는 데이터와 처리 도구를 제공합니다. | [Paper](https://arxiv.org/abs/2408.15474) · [Code (data)](https://github.com/NZqian/RapBank) · [Demo](https://nzqian.github.io/Freestyler/) |
| AlignSTS | 모달리티 간 정렬을 활용한 음성의 가창 변환. | [Paper](https://arxiv.org/abs/2305.04476) · [Code](https://github.com/RickyL-2000/AlignSTS) · [Model](https://drive.google.com/file/d/1hKesxqkbrBKC06eYLmlCutPathdJLCK1/view) |
| ExpressiveSinger | 다국어 및 다양한 스타일의 가창을 위한 표현 제어. | [Paper](https://doi.org/10.1145/3664647.3681642) · [Demo](https://expressivesinger.github.io/ExpressiveSinger/) |
| TechSinger | 플로 매칭을 활용한 다국어 가창 기법 제어. | [Paper](https://arxiv.org/abs/2502.12572) · [Code](https://github.com/gwx314/TechSinger) · [Model](https://huggingface.co/verstar/TechSinger) |
| Prompt-Singer | 자연어 프롬프트를 통한 가창 합성 제어. | [Paper](https://arxiv.org/abs/2403.11780) · [Code](https://github.com/cyanbx/Prompt-Singer) · [Model](https://huggingface.co/Cyanbox/Prompt-Singer) |

<a name="song-and-music-generation"></a>

### 노래 및 음악 생성

| 모델 | 주요 연구 내용 | 자료 |
| --- | --- | --- |
| YuE | 가사 기반 노래 생성. 링크된 브랜치는 기존 YuE 버전을 보존합니다. | [Paper](https://arxiv.org/abs/2503.08638) · [Code](https://github.com/multimodal-art-projection/YuE/tree/YuE-v1) · [Model](https://huggingface.co/m-a-p/YuE-s1-7B-anneal-en-cot) |
| InspireMusic | 음악, 노래, 오디오 생성 도구 모음. | [Paper](https://arxiv.org/abs/2503.00084) · [Code](https://github.com/FunAudioLLM/InspireMusic) · [Model (music)](https://modelscope.cn/models/iic/InspireMusic-1.5B-Long) |
| SongGen | 단일 단계 자기회귀 Transformer를 활용한 텍스트 기반 노래 생성. | [Paper](https://arxiv.org/abs/2502.13128) · [Code](https://github.com/LiuZH-19/SongGen) · [Model](https://huggingface.co/LiuZH-19/SongGen_mixed_pro) |
| DiffRhythm | 잠재 확산을 활용한 종단 간 전체 길이 노래 생성. | [Paper](https://arxiv.org/abs/2503.01183) · [Code](https://github.com/ASLP-lab/DiffRhythm) · [Model](https://huggingface.co/ASLP-lab/DiffRhythm-full) |
| Levo | 보컬과 반주를 포함한 노래 생성. | [Paper](https://arxiv.org/abs/2506.07520) · [Code](https://github.com/levo-demo/LeVo) · [Model](https://huggingface.co/lglg666/SongGeneration-base-new) |

<a name="related-speech-and-singing-models"></a>

### 관련 음성 및 가창 모델

| 모델 | 주요 연구 내용 | 자료 |
| --- | --- | --- |
| NaturalSpeech 2(비공식 구현) | 확산 기반 음성 및 가창 합성. 비공식 구현입니다. | [Paper](https://arxiv.org/abs/2304.09116) · [Code](https://github.com/lucidrains/naturalspeech2-pytorch) |
| SpeechGPT-Gen | 정보 사슬 모델링을 활용한 음성 생성. | [Paper](https://arxiv.org/abs/2401.13527) · [Repo (planned)](https://github.com/0nutation/SpeechGPT/tree/main/speechgpt-gen) · [Demo](https://0nutation.github.io/SpeechGPT-Gen.github.io/) |

---

<a name="resources-in-svs-models"></a>

## 📦 자료

이 절에서는 학습 및 평가 데이터 준비에 필요한 가창 데이터셋과 도구를 정리합니다.

<a name="open-source-datasets"></a>

### 📊 공개 데이터셋

**데이터셋 및 부가 자료 45개**를 수록하며 가창 합성 학습, 정렬·전사, 분리, 평가를 다룹니다. **Data**는 공개 데이터, **Annotations / Metadata**는 주석·출처 목록, **Access**는 신청이 필요할 수 있는 이용 안내를 뜻합니다. 논문만 있거나 공개 예정인 항목은 명시합니다. 언어 코드: zh = 중국어 표준어, en = 영어, ja = 일본어, ko = 한국어. 다른 다국어 자료는 확인 가능한 경우 언어 수를 표기합니다.

기존 코퍼스 통계는 [서베이 표 1](https://arxiv.org/html/2601.13910v1)을 바탕으로 하되 저자 공개 자료와 데이터 논문에 따라 버전 정보와 통계를 보완했습니다. 길이는 근삿값입니다. ACE의 길이는 **코퍼스 전체 합계**이며 음색 수는 합성 음색을 뜻합니다. 파생 코퍼스와 평가 하위 집합은 중복되므로 각 행을 더해 고유 오디오 총량으로 사용하지 마세요.

[가창 및 SVS 학습 코퍼스](#svs-training-corpora) · [가사·음표·곡 구조·분리 데이터](#alignment-and-separation-data) · [평가 벤치마크 및 부가 주석](#singing-evaluation-benchmarks)

<a name="svs-training-corpora"></a>

#### 가창 및 SVS 학습 코퍼스

| 데이터셋 | 언어 / 규모 | 내용 및 이용 상태 | 자료 |
| --- | --- | --- | --- |
| NUS-48E | en · 가창자 12명 | 가창 115분 + 발화 54분, 음소 경계 포함. 논문에서 코퍼스 정보 제공. | [Paper](https://ieeexplore.ieee.org/document/6694316) |
| VocalSet | en · 가창자 20명 · 10.1 h | 다양한 음높이와 맥락의 가창 기법·모음 녹음. | [Data](https://zenodo.org/records/1203819) |
| CSD | ko / en · 100곡 | 가창자 1명, 곡당 2개 조성으로 총 200개 녹음. MIDI와 음소·문자 가사 포함. | [Code](https://github.com/emotiontts/emotiontts_open_db/tree/master/Dataset/CSD) · [Data](https://zenodo.org/records/4785016) |
| PJS | ja · 가창자 1명 · 0.5 h | 음소 균형을 고려한 일본어 가창과 악보·시간 정보. | [Paper](https://arxiv.org/abs/2006.02959) · [Data](https://sites.google.com/site/shinnosuketakamichi/research-topics/pjs_corpus) |
| NHSS | en · 가창자 10명 · 7 h | 100곡의 병렬 발화·가창을 합한 길이. 이용 동의서와 이메일 신청 필요. | [Paper](https://arxiv.org/abs/2012.00337) · [Access](https://hltnus.github.io/NHSSDatabase/download.html) |
| OpenSinger | zh · 가창자 66명 · 50 h | 가창 합성·음색 변환용 다중 가창자 중국어 녹음. | [Access](https://multi-singer.github.io/) |
| Tohoku Kiritan | ja · 50곡 | 단일 가창자 녹음과 악보 자료. 제공처의 이용 절차 확인 필요. | [Access](https://zunko.jp/kiridev/login.php) |
| PopCS | zh · 가창자 1명 · 5.9 h | DiffSinger의 중국어 코퍼스. 신청 후 이용. | [Paper](https://arxiv.org/abs/2105.02446) · [Access](https://github.com/MoonInTheRiver/DiffSinger/blob/master/resources/apply_form.md) |
| M4Singer | zh · 가창자 20명 · 29.8 h | 수작업 악보·가사·음소 주석. 소프라노, 알토, 테너, 베이스 포함. | [Code](https://github.com/M4Singer/M4Singer) · [Data](https://drive.google.com/file/d/1xC37E59EWRRFFLdG3aJkVqwtLDgtFNqW/view) |
| PopBuTFy | zh / en · 가창자 34명 · 50.8 h | 가창 보정용 아마추어·전문가 녹음. NeuralSVB에서 이용 안내 제공. | [Paper](https://arxiv.org/abs/2202.13277) · [Code / Access](https://github.com/MoonInTheRiver/NeuralSVB) |
| Opencpop | zh · 가창자 1명 · 5.2 h | 음소·음표 경계가 있는 중국어 팝 가창. 양식 제출 후 이메일로 다운로드 안내. | [Paper](https://arxiv.org/abs/2201.07429) · [Access](https://wenet-e2e.github.io/opencpop/download/) |
| SingStyle111 | 3 개 언어 · 가창자 8명 · 12.8 h | 다국어 가창 스타일 코퍼스. Zenodo 접근 제한. | [Access](https://zenodo.org/records/10265401) |
| GTSinger | 9 개 언어 · 가창자 20명 · 80.6 h | 가창 기법 라벨이 있는 다국어 가창, 대응 발화 및 악보 주석. | [Paper](https://arxiv.org/abs/2409.13832) · [Code](https://github.com/GTSinger/GTSinger) · [Data](https://huggingface.co/datasets/AaronZ345/GTSinger) |
| ACE-Opencpop | zh · 30 개 음색 · 128.9 h | 실제 가창자 30명이 아닌 합성 음색. 총 128.9 h, 음색당 평균 4.3 h. | [Paper](https://arxiv.org/abs/2401.17619v2) · [Data](https://huggingface.co/datasets/espnet/ace-opencpop-segments) |
| ACE-KiSing | zh / en · 34 개 음색 · 32.5 h | 합성 가창 증강 데이터. 총 32.5 h, 음색당 약 1 h. | [Paper](https://arxiv.org/abs/2401.17619v2) · [Data](https://huggingface.co/datasets/espnet/ace-kising-segments) |
| KiSing-v1 | zh · 가창자 1명 · 0.7 h | 14곡의 원본 실녹음 코퍼스. 합성 ACE-KiSing과 구분하며 참고 논문에서 둘 다 설명. | [Reference](https://arxiv.org/abs/2401.17619v2) |
| JVS-MuSiC | ja · 가창자 100명 · 2.3 h | 가창자당 2곡. 관련 JVS 낭독 코퍼스와 함께 활용 가능. | [Paper](https://arxiv.org/abs/2001.07044) · [Data](https://sites.google.com/site/shinnosuketakamichi/research-topics/jvs_music) |
| JSUT-song | ja · 27곡 | 단일 가창자의 동요, 악보 및 음소 정렬 자료. | [Data](https://sites.google.com/site/shinnosuketakamichi/publication/jsut-song) |
| NIT-SONG070-F001 | ja · 31곡 | HTS/Sinsy 연구에 사용되는 일본어 단일 가창자 코퍼스. 비교 문헌 참조. | [Reference](https://arxiv.org/abs/2401.17619v2) |
| CrawlSinger-OS | zh · 2,317 h · 776k 구간 | 합성·실제 오디오에 가사, 음높이, 음표 길이, 템포 제공. 다른 행의 원천 데이터와 중복. | [Paper](https://arxiv.org/abs/2607.27768v1) · [Code](https://github.com/pymaster17/VocalRender) · [Data](https://huggingface.co/datasets/pymaster/CrawlSinger-OS) |
| OpenSongSong | zh · 29.9 h | SongSong(AAAI 2025)의 송사 가창 코퍼스. 다운로드 가능한 공개본은 미확인. | [Paper](https://ojs.aaai.org/index.php/AAAI/article/view/34820) · [Demo](https://zcli-charlie.github.io/projects/songsong/) |
| SingNet | 다국어 · ~3,000 h | 논문에서 소개한 자연 환경의 가창 코퍼스와 처리 파이프라인. 공개 오디오 다운로드는 미확인. | [Paper](https://arxiv.org/abs/2505.09325) |

<a name="alignment-and-separation-data"></a>

#### 가사·음표·곡 구조·분리 데이터

| 데이터셋 | 언어 / 규모 | 내용 및 이용 상태 | 자료 |
| --- | --- | --- | --- |
| KVT | ko · 가창자 114명 · 18.9 h | 가창 음색·스타일 태그. 논문에서 주석과 출처 링크를 설명하며 오디오는 재배포하지 않음. | [Paper](https://ieeexplore.ieee.org/document/9097399) |
| MIR-1K | zh · 가창자 19명 · 2.2 h | 가창 분리·음높이 연구용 보컬·반주 발췌 1,000개. | [Data](https://zenodo.org/records/3532216) |
| DAMP-MVP / Sing! 300×30×2 | 다국어 | 노래방 가창, 가사, 메타데이터. 오디오는 접근 승인 필요. | [Access](https://zenodo.org/records/2747436) |
| DSing | en · DAMP 하위 집합 | 가사 전사용 구간 분할·실험 레시피. 원본 오디오는 DAMP 승인 필요. | [Code / Annotations](https://github.com/groadabike/Kaldi-Dsing-task) · [Access](https://zenodo.org/records/2747436) |
| DALI | 다국어 (v1) · 5358곡 | 정렬된 가사·보컬 음표. 오디오 묶음 대신 주석과 오디오 검색 코드 제공. | [Paper](https://arxiv.org/abs/1906.10606) · [Code / Annotations](https://github.com/gabolsgabs/DALI) |
| RapBank | 84 개 언어 · 5,586 h (수집 규모) | 랩 영상 ID와 처리 파이프라인. 보고된 수집 규모는 호스팅된 오디오 다운로드 규모와 다름. | [Paper](https://arxiv.org/abs/2408.15474) · [Code / Metadata](https://github.com/NZqian/RapBank) |
| MIR-ST500 | 팝 · 500곡 | 보컬 음표 주석과 원본 URL 제공. 저작권 오디오는 재배포하지 않음. | [Paper](https://ieeexplore.ieee.org/document/9414601) · [Code / Annotations](https://github.com/york135/singing_transcription_ICASSP2021) |
| JamendoLyrics MultiLang | en / fr / de / es · 79곡 | 단어·행 단위 가사 타임스탬프가 있는 오디오. 현재 Hugging Face 공개본. | [Paper](https://arxiv.org/abs/2306.07744) · [Data](https://huggingface.co/datasets/jamendolyrics/jamendolyrics) |
| MuChin 1k / v2-6066 | zh (v2) · 6066곡 | 음악 설명, 구조, 가사. v2의 중복 주석 및 가사 타임스탬프 안내 확인 필요. | [Paper](https://www.ijcai.org/proceedings/2024/0860.pdf) · [Code](https://github.com/CarlWangChina/MuChin-V2-6066) · [Data](https://huggingface.co/datasets/karl-wang/MuChin-v2-6066) |
| SongFormDB | 다국어 · >10k 곡 | 4개 하위 집합의 곡 구조 라벨. 원천별 오디오 복원 절차 제공. | [Paper](https://arxiv.org/abs/2510.02797) · [Data](https://huggingface.co/datasets/ASLP-lab/SongFormDB) |
| MUSDB18 / MUSDB18-HQ | 다국어 · 150곡 | 약 10 h. 보컬·베이스·드럼·기타 스템. HQ는 동일 곡의 고음질 버전. | [Access](https://sigsep.github.io/datasets/musdb.html) · [Data (HQ)](https://zenodo.org/records/3338373) |
| DSD100 | 다국어 · 100곡 | 보컬·반주 분리용 스템. MUSDB18에도 포함. | [Data](https://sigsep.github.io/datasets/dsd100.html) |
| MedleyDB 1.0 / 2.0 | 122 + 74 개 멀티트랙 녹음 | 악기·보컬 스템과 멜로디 주석. 기악곡도 포함하며 오디오는 신청 필요. | [Access / Annotations](https://medleydb.weebly.com/) |
| jaCappella v2 | ja · 50곡 | 곡당 6개 독립 보컬 파트와 PDF/MusicXML 악보. 제공처 이용 조건 적용. | [Paper](https://arxiv.org/abs/2211.16028) · [Data](https://huggingface.co/datasets/jaCappella/jaCappella) |

<a name="singing-evaluation-benchmarks"></a>

#### 평가 벤치마크 및 부가 주석

| 데이터셋 | 언어 / 규모 | 내용 및 이용 상태 | 자료 |
| --- | --- | --- | --- |
| Annotated-VocalSet | VocalSet 부가 자료 | VocalSet 추가 주석. 독립 오디오 코퍼스로 중복 집계하지 않음. | [Annotations](https://zenodo.org/records/7061507) |
| SoulX-Singer-Eval | zh / en · 100 클립 · 50 명 가창자 | 교차 도메인 제로샷 가창 평가. 같은 공개 저장소에 GMO-SVS 802개 샘플도 포함. | [Paper](https://arxiv.org/abs/2602.07803v2) · [Code](https://github.com/Soul-AILab/SoulX-Singer-Eval) · [Data](https://huggingface.co/datasets/Soul-AILab/SoulX-Singer-Eval-Dataset) |
| LyricEditBench | zh / en · 7,200 개 사례 | GTSinger 기반 멜로디 보존 가사 편집 6개 과제. 원본 녹음과 중복. | [Paper](https://arxiv.org/abs/2603.24589) · [Code](https://github.com/ASLP-lab/YingMusic-Singer-Plus) · [Data](https://huggingface.co/datasets/ASLP-lab/LyricEditBench) |
| SCSBench | UniVocal · ACL 2026 | 말하기·노래 전환 벤치마크. 논문에 소개되었으나 공식 데이터는 공개 예정. | [Paper](https://aclanthology.org/2026.acl-long.1452/) · [Repo (planned)](https://github.com/QwenAudio/FunResearch/tree/main/UniVocal) |
| MMGenre | zh · 3,152 쌍 · 4.36 h | 합성 가창·악보 쌍. 공개 카드 기준 148곡, 10개 장르, 26개 하위 장르. | [Paper](https://arxiv.org/abs/2607.06986) · [Code](https://github.com/FengJin1117/mmgenre) · [Data](https://huggingface.co/datasets/Leaky-ReLU/MMGenre) |
| WildSongBench | zh / en · 192 개 프롬프트 | 곡 생성 프롬프트, 시드, 평가 도구. 참조 오디오는 미포함. | [Paper](https://arxiv.org/abs/2609.33757v1) · [Data (prompts)](https://huggingface.co/datasets/m-a-p/WildSongBench) |
| SingMOS / SingMOS-Pro | 주관적 품질 평가 | 사람의 품질 평가가 있는 가창 샘플. MOS 예측 및 벤치마킹용. | [Paper](https://arxiv.org/abs/2406.10911) · [Paper (Pro)](https://arxiv.org/abs/2510.01812) · [Code](https://github.com/South-Twilight/SingMOS) · [Data](https://huggingface.co/datasets/TangRain/SingMOS-v1) · [Data (Pro)](https://huggingface.co/datasets/TangRain/SingMOS-Pro) |
| SingFox | 20 개 언어 · 113,802 클립 · 126.32 h | 가창 딥페이크 탐지·출처 추적(Interspeech 2026). 구축 코드는 공개, 전체 오디오 공개본은 미확인. | [Paper](https://www.isca-archive.org/interspeech_2026/shah26_interspeech.html) · [Code](https://github.com/Arth-Shah/SingFox) |
| Jam-ALT | en / fr / de / es · 79곡 | 수정된 가사와 행별 시간 정보의 전사 벤치마크. JamendoLyrics와 동일 오디오. | [Paper](https://arxiv.org/abs/2408.06370) · [Code](https://github.com/audioshake/alt-eval) · [Data](https://huggingface.co/datasets/jamendolyrics/jam-alt) |

<a name="annotation-tools-for-singing-data"></a>

### 🛠️ 주석 및 전처리 도구

아래 자료는 가사 정렬, 보컬 음표 전사, 더 깨끗한 보컬 녹음 준비에 사용할 수 있습니다.

| 도구 | 과제 | 자료 |
| --- | --- | --- |
| MFA | 음성과 텍스트의 강제 정렬 | [Paper](https://doi.org/10.21437/Interspeech.2017-1386) · [Code](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner) |
| SOFA | 가창과 텍스트의 강제 정렬 | [Code](https://github.com/qiuqiao/SOFA) · [Model (community)](https://github.com/qiuqiao/SOFA/discussions/categories/pretrained-model-sharing) |
| VOCANO | 보컬 음표 전사 | [Paper](https://archives.ismir.net/ismir2021/paper/000036.pdf) · [Code](https://github.com/B05901022/VOCANO) |
| MusicYOLO | 음악 음표 전사 | [Code](https://github.com/itec-hust/MusicYOLO) · [Model](https://pan.baidu.com/s/1TbE36ydi-6EZXwxo5DwfLg?pwd=1234) |
| ROSVOT | 보컬 음표 전사 | [Paper](https://arxiv.org/abs/2405.09940) · [Code](https://github.com/RickyL-2000/ROSVOT) · [Model](https://drive.google.com/file/d/1JNtNT37KiLq9uFQqHk7JFs-3trxd3bRh/view) |
| STARS | 통합 주석 모델 | [Paper](https://arxiv.org/abs/2507.06670) · [Code](https://github.com/gwx314/STARS) · [Model](https://huggingface.co/verstar/STARS) |
| UVR | 보컬과 반주 분리 | [Code](https://github.com/Anjok07/ultimatevocalremovergui) · [App](https://ultimatevocalremover.com/) |
| ClearerVoice | 음성 향상 | [Paper](https://arxiv.org/abs/2506.19398) · [Code](https://github.com/modelscope/ClearerVoice-Studio) · [Model](https://modelscope.cn/models/iic/ClearerVoice-Studio) |
| SheetSage2 | 보컬 멜로디와 코드의 리드 시트 전사. 기술 보고서 공개일: 2026-10-02. | [Report](https://github.com/multimodal-art-projection/YuE/blob/main/docs/sheetsage2_technical_report.pdf) · [Code / Model](https://huggingface.co/m-a-p/SheetSage2) |

---

<a name="citation"></a>

## 📝 인용

이 저장소가 연구에 도움이 되었다면 IJCNLP-AACL 2025에 게재된 논문을 인용해 주세요.

```bibtex
@inproceedings{pan-etal-2025-synthetic,
  title = "Synthetic Singers: A Review of Deep-Learning-based Singing Voice Synthesis Approaches",
  author = "Pan, Changhao and Yao, Dongyu and Zhang, Yu and Guo, Wenxiang and Lu, Jingyu and Zhu, Zhiyuan and Zhao, Zhou",
  editor = "Inui, Kentaro and Sakti, Sakriani and Wang, Haofen and Wong, Derek F. and Bhattacharyya, Pushpak and Banerjee, Biplab and Ekbal, Asif and Chakraborty, Tanmoy and Singh, Dhirendra Pratap",
  booktitle = "Proceedings of the 14th International Joint Conference on Natural Language Processing and the 4th Conference of the Asia-Pacific Chapter of the Association for Computational Linguistics (Volume 1: Long Papers)",
  month = dec,
  year = "2025",
  address = "Mumbai, India",
  publisher = "The Asian Federation of Natural Language Processing and The Association for Computational Linguistics",
  url = "https://aclanthology.org/2025.ijcnlp-long.24/",
  pages = "396--416",
  isbn = "979-8-89176-298-5"
}
```

---

<a name="contributing"></a>

## 🤝 기여 안내

자료 추가와 오류 수정을 환영합니다. 논문, 모델, 데이터셋, 도구를 제안하려면 이름, 원 출처 링크, 가창 음성 합성과의 관련성을 설명하는 짧은 글을 포함해 [이슈](https://github.com/DaViD-Pigeon/SyntheticSingers/issues) 또는 풀 리퀘스트를 제출해 주세요. 비공식 구현 여부를 표시하고 코드, 모델 가중치, 데이터셋, 데모를 구분해 주세요.

---

<a name="license"></a>

## 📄 라이선스

이 저장소를 위해 작성한 원본 문서는 [MIT 라이선스](LICENSE)를 따릅니다. 리뷰 논문, 논문에서 가져온 그림, 링크된 제3자 논문·코드·모델 가중치·데이터셋·도구에는 각각의 라이선스가 적용됩니다.

---

<a name="update"></a>

## 🔄 업데이트 기록

**이 저장소는 매월 최소 한 번 보완하고 업데이트하겠습니다.** 관련 논문, 모델, 데이터셋, 도구를 추가하고 자료 정보를 수정하며, 각 업데이트를 이곳에 기록하겠습니다.

- **2026-10-03**: README 구성과 탐색을 정비하고 중국어·한국어·일본어판을 추가했습니다. 2026년 대표 모델 논문 12편과 SheetSage2 도구를 추가하고 데이터셋·부가 자료를 45개로 확장했습니다. Paper / Code / Model 링크와 공개 상태를 확인하고 통계를 수정했으며 기여 안내, 라이선스, 월별 업데이트 기록을 마련했습니다.
- **2026-01**: Synthetic Singers 리뷰를 [arXiv](https://arxiv.org/abs/2601.13910v1)에 공개하고 모델, 데이터셋, 주석 도구를 모은 부속 저장소를 공개했습니다.
