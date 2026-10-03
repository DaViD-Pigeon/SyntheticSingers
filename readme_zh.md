<div align="center">

# Synthetic Singers

## 基于深度学习的歌声合成方法综述

**IJCNLP-AACL 2025 · 口头报告**

Changhao Pan, Dongyu Yao, Yu Zhang, Wenxiang Guo,<br>
Jingyu Lu, Zhiyuan Zhu, Zhou Zhao

浙江大学

[![arXiv](https://img.shields.io/badge/arXiv-2601.13910-b31b1b.svg?logo=arxiv&logoColor=white)](https://arxiv.org/abs/2601.13910v1)
[![ACL Anthology](https://img.shields.io/badge/ACL%20Anthology-IJCNLP--AACL%202025-1f6feb.svg)](https://aclanthology.org/2025.ijcnlp-long.24/)
[![GitHub Stars](https://img.shields.io/github/stars/DaViD-Pigeon/SyntheticSingers?style=social)](https://github.com/DaViD-Pigeon/SyntheticSingers)

[English](README.md) · **简体中文** · [한국어](readme_kr.md) · [日本語](readme_ja.md)

**[模型](#publicly-available-singing-voice-synthesis-models) · [数据集](#open-source-datasets) · [工具](#annotation-tools-for-singing-data)**

</div>

<a name="quick-start"></a>

## 🚀 快速导览

本仓库是 **Synthetic Singers: A Review of Deep-Learning-based Singing Voice Synthesis Approaches** 的官方仓库，论文发表于 **IJCNLP-AACL 2025（口头报告）**。可通过 [ACL Anthology](https://aclanthology.org/2025.ijcnlp-long.24/) 或 [arXiv](https://arxiv.org/abs/2601.13910v1) 阅读论文。

- **任务分类。** 了解高保真合成、可控合成、歌唱风格迁移与文本到歌曲生成。
- **系统架构。** 通过综述图示理解级联式与端到端歌声合成系统的区别。
- **代表性模型。** 按主要研究方向浏览模型，查看简要说明与可用资源链接。
- **研究资源。** 查找歌声数据集、语料规模统计，以及对齐、转录、分离和增强工具。

## 目录

1. [简介](#introduction)
2. [综述框架](#overall)
3. [歌声合成任务](#tasks-of-svs)
4. [歌声合成系统架构](#architectures-of-svs-systems)
5. [代表性模型与资源](#publicly-available-singing-voice-synthesis-models)
   - [2026 年代表工作（1–10 月）](#highlights-2026)
   - [歌声合成与声码器](#singing-synthesis-and-vocoders)
   - [风格控制与迁移](#style-control-and-transfer)
   - [歌曲与音乐生成](#song-and-music-generation)
   - [相关语音与歌声模型](#related-speech-and-singing-models)
6. [资源](#resources-in-svs-models)
   - [可用数据集](#open-source-datasets)
   - [标注与预处理工具](#annotation-tools-for-singing-data)
7. [引用](#citation)
8. [参与贡献](#contributing)
9. [许可证](#license)
10. [更新记录](#update)

---

<a name="introduction"></a>

## 📌 简介

**Synthetic Singers** 汇集了基于深度学习的歌声合成任务、架构、模型与数据资源。本仓库配套我们的[综述论文](https://aclanthology.org/2025.ijcnlp-long.24/)，为研究人员与实践者提供实用的阅读导览。

概览图展示综述的组织结构与技术视角；资源表将这些视角对应到具体项目，帮助读者定位相关系统并准备歌声数据。

---

<a name="overall"></a>

## 🧭 综述框架

<div align="center">
  <img src="figure/organization.png" alt="Synthetic Singers 综述的整体结构" width="90%">
  <p><em>图 1. Synthetic Singers 综述的整体结构。</em></p>
</div>

---

<a name="tasks-of-svs"></a>

## 🎯 歌声合成任务

本综述将歌声合成分为四类任务，一个系统可以同时支持多类任务。

| 任务 | 主要目标 | 重点关注 |
| --- | --- | --- |
| **高保真合成** | 生成清晰、自然且符合歌词与旋律的歌声。 | 音质、歌词可懂度与音准。 |
| **可控合成** | 在保持合成质量的同时调节歌唱属性。 | 音色、风格、表现力与演唱技巧的控制。 |
| **歌唱风格迁移** | 复现参考演唱中的声音特征。 | 从参考音频迁移音色、风格与表现力。 |
| **文本到歌曲生成** | 根据文本输入生成完整歌曲。 | 人声、伴奏与音乐结构的一致性。 |

<div align="center">
  <img src="figure/tasks.png" alt="歌声合成任务概览" width="90%">
  <p><em>图 2. 歌声合成的四类代表性任务。</em></p>
</div>

---

<a name="architectures-of-svs-systems"></a>

## 🏗️ 歌声合成系统架构

根据波形生成是否依赖独立声码器，我们区分以下两类架构范式。

| 范式 | 合成流程 | 主要组件 |
| --- | --- | --- |
| **级联式歌声合成** | 先预测声学特征，再将其转换为波形。 | 声学模型与独立声码器。 |
| **端到端歌声合成** | 在一体化合成系统中生成波形。 | 联合建模条件信息、中间表示与波形生成。 |

<div align="center">
  <img src="figure/arch.png" alt="歌声合成系统的架构范式" width="90%">
  <p><em>图 3. 级联式与端到端歌声合成架构。虚线表示可选组件。</em></p>
</div>

---

<a name="publicly-available-singing-voice-synthesis-models"></a>

## 📚 代表性模型与资源

模型按主要研究方向分组，能力可能交叉。**Paper** 指论文或预印本，**Code** 指实现代码，**Model** 指权重或其下载说明，**Demo** 指演示；**Repo (planned)** 表示官方待发布仓库，不代表代码或权重已经公开。仅列出已核实的资源类型，缺少链接不等于确定未发布。非官方实现以及 **Model (TTS)** 等限定版本均单独标注。

<a name="highlights-2026"></a>

### 2026 年代表工作（1–10 月）

**收录范围：2026-01-01 至 2026-10-03。** 本次新增 12 篇，覆盖乐谱驱动歌声合成、语音／歌声切换、歌词编辑与完整歌曲生成。月份以论文首次公开时间为准，不一定等于代码或权重发布时间。会议标签以正式论文集为依据，其余为预印本或技术报告；旧论文的 2026 年修订版不作为新工作计入。

| 工作 | 首次论文／会议 | 研究重点 | 资源 |
| --- | --- | --- | --- |
| HeartMuLa | 2026-01 · 预印本／技术报告 | 以歌词、风格描述与参考音频为条件生成歌曲，配套低帧率音乐编解码器。 | [Paper](https://arxiv.org/abs/2601.10547v3) · [Code](https://github.com/HeartMuLa/heartlib) · [Model](https://huggingface.co/HeartMuLa/HeartMuLa-oss-3B-happy-new-year) |
| ACE-Step 1.5 | 2026-01 · 预印本／技术报告 | 结合语言模型歌曲规划与扩散生成，支持编辑和轻量个性化适配。 | [Paper](https://arxiv.org/abs/2602.00744v3) · [Code](https://github.com/ace-step/ACE-Step-1.5) · [Model](https://huggingface.co/ACE-Step/Ace-Step1.5) |
| SoulX-Singer | 2026-02 · 预印本／技术报告 | 由乐谱或旋律驱动的零样本歌声合成，支持普通话、英语和粤语。 | [Paper](https://arxiv.org/abs/2602.07803v2) · [Code](https://github.com/Soul-AILab/SoulX-Singer) · [Model](https://huggingface.co/Soul-AILab/SoulX-Singer) |
| YingMusic-Singer / Plus | 2026-03 · Interspeech 2026 | 无需手工对齐的保旋律歌词编辑；代码和权重链接指向后续 Plus 版本。 | [Paper](https://www.isca-archive.org/interspeech_2026/hao26_interspeech.html) · [Preprint](https://arxiv.org/abs/2603.24589) · [Code](https://github.com/ASLP-lab/YingMusic-Singer-Plus) · [Model](https://huggingface.co/ASLP-lab/YingMusic-Singer-Plus) |
| UniVocal | 2026-06 · ACL 2026 | 文本控制的语音／歌声切换；官方仓库中的代码、权重及 SCSBench 仍为待发布。 | [Paper](https://aclanthology.org/2026.acl-long.1452/) · [Repo (planned)](https://github.com/QwenAudio/FunResearch/tree/main/UniVocal) · [Demo](https://project-univocal-demo.github.io/demo/) |
| UniVoice | 2026-06 · 预印本／技术报告 | 统一语音与歌声的流匹配框架，分别建模内容、旋律与音色条件。 | [Paper](https://arxiv.org/abs/2606.05852v1) |
| MeloDISinger | 2026-06 · Interspeech 2026 | 通过流匹配补全编辑歌词，同时保留旋律、时长与未编辑区域。 | [Paper](https://www.isca-archive.org/interspeech_2026/park26k_interspeech.html) · [Preprint](https://arxiv.org/abs/2606.30580v1) · [Demo](https://cottonlove.github.io/MeloDISinger_demo/) |
| LeVo 2 | 2026-06 · 预印本／技术报告 | 分层歌曲建模，结合人声／伴奏双流与扩散音乐编解码器。 | [Paper](https://arxiv.org/abs/2606.30642v1) · [Code](https://github.com/levo-demo/LeVo) · [Model](https://huggingface.co/lglg666/SongGeneration-v2-large) |
| Qwen-Music | 2026-07 · 预印本／技术报告 | 结合 Melody-CoT 规划与流匹配音频生成，支持歌曲生成和翻唱。 | [Paper](https://arxiv.org/abs/2607.11699v3) |
| VocalRender | 2026-07 · 预印本／技术报告 | 以歌词、音高、音符时值与速度为输入，通过自回归扩散直接实现乐谱驱动的歌声合成。 | [Paper](https://arxiv.org/abs/2607.27768v1) · [Code](https://github.com/pymaster17/VocalRender) · [Model](https://huggingface.co/pymaster/VocalRender) · [Data](https://huggingface.co/datasets/pymaster/CrawlSinger-OS) |
| DiffSynth-Music | 2026-09 · 预印本／技术报告 | 基于 ACE-Step，利用音频条件控制节拍、人声、伴奏、韵律与参考音色。 | [Paper](https://arxiv.org/abs/2609.12774v1) · [Code](https://github.com/modelscope/DiffSynth-Studio/tree/main/examples/diffsynth_music) · [Model](https://modelscope.cn/models/DiffSynth-Studio/DiffSynth-Music) |
| YuE2 | 2026-09 · 预印本／技术报告 | 先规划可编辑的旋律与和弦，再生成完整歌曲音频，并支持零样本翻唱。 | [Paper](https://arxiv.org/abs/2609.33757v1) · [Code](https://github.com/multimodal-art-projection/YuE) · [Model](https://huggingface.co/m-a-p/YuE2-3B) |

<a name="singing-synthesis-and-vocoders"></a>

### 歌声合成与声码器

| 模型 | 研究重点 | 资源 |
| --- | --- | --- |
| DiffSinger | 基于浅层扩散的歌声合成。 | [Paper](https://arxiv.org/abs/2105.02446) · [Code](https://github.com/MoonInTheRiver/DiffSinger) · [Model](https://github.com/MoonInTheRiver/DiffSinger/releases) |
| VISinger（非官方实现） | 结合变分推断与对抗学习的端到端歌声合成。 | [Paper](https://arxiv.org/abs/2110.08813) · [Code](https://github.com/So-Fann/VISinger) |
| VISinger 2 | 利用数字信号处理合成器增强端到端合成。 | [Paper](https://arxiv.org/abs/2211.02903) · [Code](https://github.com/zhangyongmao/VISinger2) · [Model](https://drive.google.com/file/d/1MgXLQuquPT2qu1__JNF010-tg48N0hZn/view) |
| VI-SVS | 基于 VITS 的歌声合成。 | [Code](https://github.com/PlayVoice/VI-SVS) · [Model](https://github.com/PlayVoice/VI-SVS/releases/tag/0.0.3) |
| NNSVS | 面向研究的神经网络歌声合成工具库。 | [Paper](https://arxiv.org/abs/2210.15987) · [Code](https://github.com/nnsvs/nnsvs) |
| CoMoSpeech | 基于一致性模型的单步语音与歌声合成。 | [Paper](https://arxiv.org/abs/2305.06908) · [Code](https://github.com/zhenye234/CoMoSpeech) · [Model (TTS)](https://drive.google.com/drive/folders/1rkbzl9NzS_fKtMubQ7FgSdgt7v8ZuYGk) |
| HiFiSinger | 高保真神经歌声合成；链接指向 Muzic 研究概览。 | [Paper](https://arxiv.org/abs/2009.01776) · [Overview](https://github.com/microsoft/muzic) |
| HiFiSinger（非官方实现） | HiFiSinger 的独立复现。 | [Paper](https://arxiv.org/abs/2009.01776) · [Code](https://github.com/CODEJIN/HiFiSinger) |
| ByteSing | 结合时长建模与 WaveRNN 声码器的中文歌声合成。 | [Paper](https://arxiv.org/abs/2004.11012) |
| WeSinger | 结合数据增强与辅助损失的歌声合成。 | [Paper](https://arxiv.org/abs/2203.10750) · [Demo](https://zzw922cn.github.io/wesinger/) |
| SingGAN | 面向高保真歌声的对抗式波形生成。 | [Paper](https://arxiv.org/abs/2110.07468) · [Demo](https://singgan.github.io/) |
| UniSinger | 通过跨模态信息匹配实现统一的端到端歌声合成。 | [Paper](https://doi.org/10.1145/3581783.3612150) · [Repo (planned)](https://github.com/ViEm-ccy/UniSinger) · [Demo](https://unisinger.github.io/Samples/) |
| Learn2Sing 2.0 | 从歌唱者的演唱中学习，生成目标说话人的歌声。 | [Paper](https://arxiv.org/abs/2203.16408) · [Code](https://github.com/WelkinYang/Learn2Sing2.0) · [Demo](https://welkinyang.github.io/Learn2Sing2.0/) |
| UniSyn | 统一的端到端文本转语音与歌声合成。 | [Paper](https://arxiv.org/abs/2212.01546) |

<a name="style-control-and-transfer"></a>

### 风格控制与迁移

| 模型 | 研究重点 | 资源 |
| --- | --- | --- |
| StyleSinger | 面向域外歌声的风格迁移。 | [Paper](https://arxiv.org/abs/2312.10741) · [Code](https://github.com/AaronZ345/StyleSinger) · [Model](https://huggingface.co/AaronZ345/StyleSinger) |
| TCSinger | 支持风格迁移与多层次风格控制的零样本歌声合成。 | [Paper](https://aclanthology.org/2024.emnlp-main.117/) · [Code](https://github.com/AaronZ345/TCSinger) · [Model](https://huggingface.co/AaronZ345/TCSinger) |
| TCSinger 2 | 可定制的多语言零样本歌声合成。 | [Paper](https://arxiv.org/abs/2505.14910) · [Code](https://github.com/AaronZ345/TCSinger2) |
| FreeStyler | 说唱生成；链接中的 RapBank 仓库提供数据与处理工具。 | [Paper](https://arxiv.org/abs/2408.15474) · [Code (data)](https://github.com/NZqian/RapBank) · [Demo](https://nzqian.github.io/Freestyler/) |
| AlignSTS | 通过跨模态对齐实现语音到歌声转换。 | [Paper](https://arxiv.org/abs/2305.04476) · [Code](https://github.com/RickyL-2000/AlignSTS) · [Model](https://drive.google.com/file/d/1hKesxqkbrBKC06eYLmlCutPathdJLCK1/view) |
| ExpressiveSinger | 面向多语言、多风格歌声的表现力控制。 | [Paper](https://doi.org/10.1145/3664647.3681642) · [Demo](https://expressivesinger.github.io/ExpressiveSinger/) |
| TechSinger | 基于流匹配的多语言演唱技巧控制。 | [Paper](https://arxiv.org/abs/2502.12572) · [Code](https://github.com/gwx314/TechSinger) · [Model](https://huggingface.co/verstar/TechSinger) |
| Prompt-Singer | 通过自然语言提示控制歌声合成。 | [Paper](https://arxiv.org/abs/2403.11780) · [Code](https://github.com/cyanbx/Prompt-Singer) · [Model](https://huggingface.co/Cyanbox/Prompt-Singer) |

<a name="song-and-music-generation"></a>

### 歌曲与音乐生成

| 模型 | 研究重点 | 资源 |
| --- | --- | --- |
| YuE | 歌词到歌曲生成；链接分支保留原始 YuE 版本。 | [Paper](https://arxiv.org/abs/2503.08638) · [Code](https://github.com/multimodal-art-projection/YuE/tree/YuE-v1) · [Model](https://huggingface.co/m-a-p/YuE-s1-7B-anneal-en-cot) |
| InspireMusic | 音乐、歌曲与音频生成工具包。 | [Paper](https://arxiv.org/abs/2503.00084) · [Code](https://github.com/FunAudioLLM/InspireMusic) · [Model (music)](https://modelscope.cn/models/iic/InspireMusic-1.5B-Long) |
| SongGen | 基于单阶段自回归 Transformer 的文本到歌曲生成。 | [Paper](https://arxiv.org/abs/2502.13128) · [Code](https://github.com/LiuZH-19/SongGen) · [Model](https://huggingface.co/LiuZH-19/SongGen_mixed_pro) |
| DiffRhythm | 基于潜空间扩散的端到端完整歌曲生成。 | [Paper](https://arxiv.org/abs/2503.01183) · [Code](https://github.com/ASLP-lab/DiffRhythm) · [Model](https://huggingface.co/ASLP-lab/DiffRhythm-full) |
| Levo | 包含人声与伴奏的歌曲生成。 | [Paper](https://arxiv.org/abs/2506.07520) · [Code](https://github.com/levo-demo/LeVo) · [Model](https://huggingface.co/lglg666/SongGeneration-base-new) |

<a name="related-speech-and-singing-models"></a>

### 相关语音与歌声模型

| 模型 | 研究重点 | 资源 |
| --- | --- | --- |
| NaturalSpeech 2（非官方实现） | 基于扩散的语音与歌声合成；链接为非官方实现。 | [Paper](https://arxiv.org/abs/2304.09116) · [Code](https://github.com/lucidrains/naturalspeech2-pytorch) |
| SpeechGPT-Gen | 基于信息链建模的语音生成。 | [Paper](https://arxiv.org/abs/2401.13527) · [Repo (planned)](https://github.com/0nutation/SpeechGPT/tree/main/speechgpt-gen) · [Demo](https://0nutation.github.io/SpeechGPT-Gen.github.io/) |

---

<a name="resources-in-svs-models"></a>

## 📦 资源

本节汇总用于准备训练与评测数据的歌声数据集和工具。

<a name="open-source-datasets"></a>

### 📊 可用数据集

**共 45 项数据集与配套资源**，覆盖歌声合成训练、对齐／转录、分离与评测。**Data** 表示已发布数据，**Annotations / Metadata** 表示标注或来源列表，**Access** 指获取说明（可能需申请）；仅有论文或待发布的条目均明确说明。语言代码：zh = 普通话，en = 英语，ja = 日语，ko = 韩语；其他多语言语料在可核实时标出语言数。

原有语料统计以[综述表 1](https://arxiv.org/html/2601.13910v1)为起点，并根据链接中的作者发布页和数据论文补充版本信息、修正统计。时长均为近似值；ACE 时长为**语料总量**，音色数表示合成音色。衍生语料与评测子集存在重叠，不能将各行简单相加作为独立音频总量。

[歌声与 SVS 训练语料](#svs-training-corpora) · [歌词、音符、歌曲结构与分离数据](#alignment-and-separation-data) · [评测基准与配套标注](#singing-evaluation-benchmarks)

<a name="svs-training-corpora"></a>

#### 歌声与 SVS 训练语料

| 数据集 | 语言／规模 | 内容与获取状态 | 资源 |
| --- | --- | --- | --- |
| NUS-48E | en · 12 位歌手 | 115 分钟歌声 + 54 分钟语音，带音素边界；论文提供语料说明。 | [Paper](https://ieeexplore.ieee.org/document/6694316) |
| VocalSet | en · 20 位歌手 · 10.1 h | 多种音高与上下文中的演唱技巧和元音录音。 | [Data](https://zenodo.org/records/1203819) |
| CSD | ko / en · 100 首歌曲 | 1 位歌手，每首 2 个调，共 200 段录音；含 MIDI 与音素／字素歌词。 | [Code](https://github.com/emotiontts/emotiontts_open_db/tree/master/Dataset/CSD) · [Data](https://zenodo.org/records/4785016) |
| PJS | ja · 1 位歌手 · 0.5 h | 音素平衡的日语歌声，配套乐谱与时间标注资源。 | [Paper](https://arxiv.org/abs/2006.02959) · [Data](https://sites.google.com/site/shinnosuketakamichi/research-topics/pjs_corpus) |
| NHSS | en · 10 位歌手 · 7 h | 总量包含 100 首歌的平行语音与歌声；需提交许可表并邮件申请。 | [Paper](https://arxiv.org/abs/2012.00337) · [Access](https://hltnus.github.io/NHSSDatabase/download.html) |
| OpenSinger | zh · 66 位歌手 · 50 h | 用于歌声合成与音色转换的多歌手普通话录音。 | [Access](https://multi-singer.github.io/) |
| Tohoku Kiritan | ja · 50 首歌曲 | 单歌手录音与乐谱资源；按提供方说明获取。 | [Access](https://zunko.jp/kiridev/login.php) |
| PopCS | zh · 1 位歌手 · 5.9 h | DiffSinger 的普通话语料，需申请获取。 | [Paper](https://arxiv.org/abs/2105.02446) · [Access](https://github.com/MoonInTheRiver/DiffSinger/blob/master/resources/apply_form.md) |
| M4Singer | zh · 20 位歌手 · 29.8 h | 人工乐谱、歌词与音素标注，覆盖女高、女低、男高、男低声部。 | [Code](https://github.com/M4Singer/M4Singer) · [Data](https://drive.google.com/file/d/1xC37E59EWRRFFLdG3aJkVqwtLDgtFNqW/view) |
| PopBuTFy | zh / en · 34 位歌手 · 50.8 h | 面向歌声美化的业余与专业演唱，获取说明见 NeuralSVB。 | [Paper](https://arxiv.org/abs/2202.13277) · [Code / Access](https://github.com/MoonInTheRiver/NeuralSVB) |
| Opencpop | zh · 1 位歌手 · 5.2 h | 带音素／音符边界的普通话流行歌声；提交表单后邮件获取下载说明。 | [Paper](https://arxiv.org/abs/2201.07429) · [Access](https://wenet-e2e.github.io/opencpop/download/) |
| SingStyle111 | 3 种语言 · 8 位歌手 · 12.8 h | 多语言演唱风格语料；Zenodo 记录为受限访问。 | [Access](https://zenodo.org/records/10265401) |
| GTSinger | 9 种语言 · 20 位歌手 · 80.6 h | 带演唱技巧标签的多语言歌声，含配对语音及乐谱标注。 | [Paper](https://arxiv.org/abs/2409.13832) · [Code](https://github.com/GTSinger/GTSinger) · [Data](https://huggingface.co/datasets/AaronZ345/GTSinger) |
| ACE-Opencpop | zh · 30 个音色 · 128.9 h | 合成音色，并非 30 位真人歌手；128.9 h 为总量，4.3 h 为单音色平均。 | [Paper](https://arxiv.org/abs/2401.17619v2) · [Data](https://huggingface.co/datasets/espnet/ace-opencpop-segments) |
| ACE-KiSing | zh / en · 34 个音色 · 32.5 h | 合成歌声扩增；32.5 h 为总量，单音色约 1 h。 | [Paper](https://arxiv.org/abs/2401.17619v2) · [Data](https://huggingface.co/datasets/espnet/ace-kising-segments) |
| KiSing-v1 | zh · 1 位歌手 · 0.7 h | 14 首歌曲的原始真人录音，与合成 ACE-KiSing 区分；参考论文介绍两者。 | [Reference](https://arxiv.org/abs/2401.17619v2) |
| JVS-MuSiC | ja · 100 位歌手 · 2.3 h | 每位歌手 2 首歌曲，可与关联的 JVS 朗读语料结合。 | [Paper](https://arxiv.org/abs/2001.07044) · [Data](https://sites.google.com/site/shinnosuketakamichi/research-topics/jvs_music) |
| JSUT-song | ja · 27 首歌曲 | 单歌手童谣，配套乐谱与音素对齐资源。 | [Data](https://sites.google.com/site/shinnosuketakamichi/publication/jsut-song) |
| NIT-SONG070-F001 | ja · 31 首歌曲 | 用于 HTS／Sinsy 研究的日语单歌手语料，详见对比参考文献。 | [Reference](https://arxiv.org/abs/2401.17619v2) |
| CrawlSinger-OS | zh · 2,317 h · 776k 片段 | 合成与真实音频混合，含歌词、音高、音符时值和速度；与其他列出语料存在来源重叠。 | [Paper](https://arxiv.org/abs/2607.27768v1) · [Code](https://github.com/pymaster17/VocalRender) · [Data](https://huggingface.co/datasets/pymaster/CrawlSinger-OS) |
| OpenSongSong | zh · 29.9 h | SongSong（AAAI 2025）介绍的宋词歌唱语料；未核实到可下载版本。 | [Paper](https://ojs.aaai.org/index.php/AAAI/article/view/34820) · [Demo](https://zcli-charlie.github.io/projects/songsong/) |
| SingNet | 多语言 · ~3,000 h | 论文介绍的开放场景歌声语料与处理流程；未核实到公开音频下载。 | [Paper](https://arxiv.org/abs/2505.09325) |

<a name="alignment-and-separation-data"></a>

#### 歌词、音符、歌曲结构与分离数据

| 数据集 | 语言／规模 | 内容与获取状态 | 资源 |
| --- | --- | --- | --- |
| KVT | ko · 114 位歌手 · 18.9 h | 歌声音色／风格标签；论文介绍标注和来源链接，不直接再分发音频。 | [Paper](https://ieeexplore.ieee.org/document/9097399) |
| MIR-1K | zh · 19 位歌手 · 2.2 h | 1,000 段人声／伴奏片段，用于歌声分离和音高研究。 | [Data](https://zenodo.org/records/3532216) |
| DAMP-MVP / Sing! 300×30×2 | 多语言 | 卡拉 OK 演唱、歌词与元数据；音频需申请访问。 | [Access](https://zenodo.org/records/2747436) |
| DSing | en · DAMP 子集 | 歌词转录切分与实验配置；原始音频需通过 DAMP 申请。 | [Code / Annotations](https://github.com/groadabike/Kaldi-Dsing-task) · [Access](https://zenodo.org/records/2747436) |
| DALI | 多语言 (v1) · 5358 首歌曲 | 对齐的歌词与人声音符；提供标注和音频获取代码，不直接打包音频。 | [Paper](https://arxiv.org/abs/1906.10606) · [Code / Annotations](https://github.com/gabolsgabs/DALI) |
| RapBank | 84 种语言 · 5,586 h （采集规模） | 说唱视频 ID 与处理流程；报告的采集总量并非托管音频下载量。 | [Paper](https://arxiv.org/abs/2408.15474) · [Code / Metadata](https://github.com/NZqian/RapBank) |
| MIR-ST500 | 流行歌曲 · 500 首歌曲 | 人声音符标注及来源 URL，不直接再分发版权音频。 | [Paper](https://ieeexplore.ieee.org/document/9414601) · [Code / Annotations](https://github.com/york135/singing_transcription_ICASSP2021) |
| JamendoLyrics MultiLang | en / fr / de / es · 79 首歌曲 | 带单词级和行级歌词时间戳的音频；链接为当前 Hugging Face 版本。 | [Paper](https://arxiv.org/abs/2306.07744) · [Data](https://huggingface.co/datasets/jamendolyrics/jamendolyrics) |
| MuChin 1k / v2-6066 | zh (v2) · 6066 首歌曲 | 音乐描述、结构与歌词；需留意 v2 说明中的重复标注和歌词时间戳问题。 | [Paper](https://www.ijcai.org/proceedings/2024/0860.pdf) · [Code](https://github.com/CarlWangChina/MuChin-V2-6066) · [Data](https://huggingface.co/datasets/karl-wang/MuChin-v2-6066) |
| SongFormDB | 多语言 · >10k 首曲目 | 4 个子集的歌曲结构标注；音频按各来源说明重建。 | [Paper](https://arxiv.org/abs/2510.02797) · [Data](https://huggingface.co/datasets/ASLP-lab/SongFormDB) |
| MUSDB18 / MUSDB18-HQ | 多语言 · 150 首歌曲 | 约 10 h，含人声、贝斯、鼓与其他分轨；HQ 为同一批歌曲的高质量版本。 | [Access](https://sigsep.github.io/datasets/musdb.html) · [Data (HQ)](https://zenodo.org/records/3338373) |
| DSD100 | 多语言 · 100 首歌曲 | 人声／伴奏分离分轨；亦被 MUSDB18 收录。 | [Data](https://sigsep.github.io/datasets/dsd100.html) |
| MedleyDB 1.0 / 2.0 | 122 + 74 首多轨录音 | 乐器／人声分轨与旋律标注，亦包含纯器乐曲；音频需申请。 | [Access / Annotations](https://medleydb.weebly.com/) |
| jaCappella v2 | ja · 50 首歌曲 | 每首 6 个独立声部分轨，含 PDF／MusicXML 乐谱；遵循提供方条款。 | [Paper](https://arxiv.org/abs/2211.16028) · [Data](https://huggingface.co/datasets/jaCappella/jaCappella) |

<a name="singing-evaluation-benchmarks"></a>

#### 评测基准与配套标注

| 数据集 | 语言／规模 | 内容与获取状态 | 资源 |
| --- | --- | --- | --- |
| Annotated-VocalSet | VocalSet 配套资源 | VocalSet 的补充标注，不应重复计为独立音频语料。 | [Annotations](https://zenodo.org/records/7061507) |
| SoulX-Singer-Eval | zh / en · 100 片段 · 50 位歌手 | 跨域零样本歌声合成评测；同一发布库另含 802 条 GMO-SVS 子集样本。 | [Paper](https://arxiv.org/abs/2602.07803v2) · [Code](https://github.com/Soul-AILab/SoulX-Singer-Eval) · [Data](https://huggingface.co/datasets/Soul-AILab/SoulX-Singer-Eval-Dataset) |
| LyricEditBench | zh / en · 7,200 条样本 | 基于 GTSinger 构建的 6 类保旋律歌词编辑任务，与原语料录音重叠。 | [Paper](https://arxiv.org/abs/2603.24589) · [Code](https://github.com/ASLP-lab/YingMusic-Singer-Plus) · [Data](https://huggingface.co/datasets/ASLP-lab/LyricEditBench) |
| SCSBench | UniVocal · ACL 2026 | 语音／歌声切换基准；论文已介绍，官方数据仍为待发布。 | [Paper](https://aclanthology.org/2026.acl-long.1452/) · [Repo (planned)](https://github.com/QwenAudio/FunResearch/tree/main/UniVocal) |
| MMGenre | zh · 3,152 对 · 4.36 h | 合成歌声／乐谱配对：发布卡片统计为 148 首歌、10 类曲风和 26 个子类。 | [Paper](https://arxiv.org/abs/2607.06986) · [Code](https://github.com/FengJin1117/mmgenre) · [Data](https://huggingface.co/datasets/Leaky-ReLU/MMGenre) |
| WildSongBench | zh / en · 192 条提示 | 歌曲生成提示词、随机种子与评测工具；不包含参考音频。 | [Paper](https://arxiv.org/abs/2609.33757v1) · [Data (prompts)](https://huggingface.co/datasets/m-a-p/WildSongBench) |
| SingMOS / SingMOS-Pro | 主观质量评测 | 带人工质量评分的歌声样本，用于 MOS 预测与评测。 | [Paper](https://arxiv.org/abs/2406.10911) · [Paper (Pro)](https://arxiv.org/abs/2510.01812) · [Code](https://github.com/South-Twilight/SingMOS) · [Data](https://huggingface.co/datasets/TangRain/SingMOS-v1) · [Data (Pro)](https://huggingface.co/datasets/TangRain/SingMOS-Pro) |
| SingFox | 20 种语言 · 113,802 片段 · 126.32 h | 歌声伪造检测与来源追踪（Interspeech 2026）；构建代码公开，完整音频发布未核实。 | [Paper](https://www.isca-archive.org/interspeech_2026/shah26_interspeech.html) · [Code](https://github.com/Arth-Shah/SingFox) |
| Jam-ALT | en / fr / de / es · 79 首歌曲 | 修订歌词文本与行级时间戳的歌词转录基准，与 JamendoLyrics 使用同一批音频。 | [Paper](https://arxiv.org/abs/2408.06370) · [Code](https://github.com/audioshake/alt-eval) · [Data](https://huggingface.co/datasets/jamendolyrics/jam-alt) |

<a name="annotation-tools-for-singing-data"></a>

### 🛠️ 标注与预处理工具

以下资源可用于歌词对齐、人声音符转录，以及更干净的人声录音准备。

| 工具 | 任务 | 资源 |
| --- | --- | --- |
| MFA | 语音与文本强制对齐 | [Paper](https://doi.org/10.21437/Interspeech.2017-1386) · [Code](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner) |
| SOFA | 歌声与文本强制对齐 | [Code](https://github.com/qiuqiao/SOFA) · [Model (community)](https://github.com/qiuqiao/SOFA/discussions/categories/pretrained-model-sharing) |
| VOCANO | 人声音符转录 | [Paper](https://archives.ismir.net/ismir2021/paper/000036.pdf) · [Code](https://github.com/B05901022/VOCANO) |
| MusicYOLO | 音乐音符转录 | [Code](https://github.com/itec-hust/MusicYOLO) · [Model](https://pan.baidu.com/s/1TbE36ydi-6EZXwxo5DwfLg?pwd=1234) |
| ROSVOT | 人声音符转录 | [Paper](https://arxiv.org/abs/2405.09940) · [Code](https://github.com/RickyL-2000/ROSVOT) · [Model](https://drive.google.com/file/d/1JNtNT37KiLq9uFQqHk7JFs-3trxd3bRh/view) |
| STARS | 统一标注模型 | [Paper](https://arxiv.org/abs/2507.06670) · [Code](https://github.com/gwx314/STARS) · [Model](https://huggingface.co/verstar/STARS) |
| UVR | 人声与伴奏分离 | [Code](https://github.com/Anjok07/ultimatevocalremovergui) · [App](https://ultimatevocalremover.com/) |
| ClearerVoice | 人声增强 | [Paper](https://arxiv.org/abs/2506.19398) · [Code](https://github.com/modelscope/ClearerVoice-Studio) · [Model](https://modelscope.cn/models/iic/ClearerVoice-Studio) |
| SheetSage2 | 人声旋律与和弦的主旋律谱转录；技术报告发布于 2026-10-02。 | [Report](https://github.com/multimodal-art-projection/YuE/blob/main/docs/sheetsage2_technical_report.pdf) · [Code / Model](https://huggingface.co/m-a-p/SheetSage2) |

---

<a name="citation"></a>

## 📝 引用

如果本仓库对您的研究有帮助，请引用正式发表于 IJCNLP-AACL 2025 的论文：

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

## 🤝 参与贡献

欢迎补充资源与纠正错误。如需推荐论文、模型、数据集或工具，请提交 [Issue](https://github.com/DaViD-Pigeon/SyntheticSingers/issues) 或 Pull Request，附上名称、一手来源链接，以及与歌声合成相关的简短说明。请标明非官方实现，并区分代码、模型权重、数据集与演示。

---

<a name="license"></a>

## 📄 许可证

为本仓库编写的原创文档采用 [MIT 许可证](LICENSE)。综述论文、转载自论文的图示，以及链接的第三方论文、代码、模型权重、数据集和工具，仍遵循各自的许可证。

---

<a name="update"></a>

## 🔄 更新记录

**我们承诺每月至少补充和更新一次本仓库**，持续收录相关论文、模型、数据集与工具，修正资源信息，并在此记录每次更新。

- **2026-10-03**：统一 README 排版与导航，新增中、韩、日文版本；补充 12 篇 2026 年代表模型论文和 SheetSage2 工具，将数据集与配套资源扩展至 45 项；完善 Paper / Code / Model 链接，核实发布状态并修正语料统计，补充贡献指南、许可证与每月更新记录。
- **2026-01**：在 [arXiv](https://arxiv.org/abs/2601.13910v1) 发布 Synthetic Singers 综述，并公开配套仓库，汇集模型、数据集与标注工具资源。
