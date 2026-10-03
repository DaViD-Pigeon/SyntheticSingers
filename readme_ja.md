<div align="center">

# Synthetic Singers

## 深層学習に基づく歌声合成手法のレビュー

**IJCNLP-AACL 2025 · 口頭発表**

Changhao Pan, Dongyu Yao, Yu Zhang, Wenxiang Guo,<br>
Jingyu Lu, Zhiyuan Zhu, Zhou Zhao

浙江大学

[![arXiv](https://img.shields.io/badge/arXiv-2601.13910-b31b1b.svg?logo=arxiv&logoColor=white)](https://arxiv.org/abs/2601.13910v1)
[![ACL Anthology](https://img.shields.io/badge/ACL%20Anthology-IJCNLP--AACL%202025-1f6feb.svg)](https://aclanthology.org/2025.ijcnlp-long.24/)
[![GitHub Stars](https://img.shields.io/github/stars/DaViD-Pigeon/SyntheticSingers?style=social)](https://github.com/DaViD-Pigeon/SyntheticSingers)

[English](README.md) · [简体中文](readme_zh.md) · [한국어](readme_kr.md) · **日本語**

**[モデル](#publicly-available-singing-voice-synthesis-models) · [データセット](#open-source-datasets) · [ツール](#annotation-tools-for-singing-data)**

</div>

<a name="quick-start"></a>

## 🚀 クイックガイド

本リポジトリは **Synthetic Singers: A Review of Deep-Learning-based Singing Voice Synthesis Approaches** の公式リポジトリです。本論文は **IJCNLP-AACL 2025 で口頭発表**されました。[ACL Anthology](https://aclanthology.org/2025.ijcnlp-long.24/) または [arXiv](https://arxiv.org/abs/2601.13910v1) でご覧いただけます。

- **タスク分類。** 高忠実度合成、制御可能な合成、歌唱スタイル変換、テキストからの楽曲生成を整理します。
- **システム構成。** 図を通じて、カスケード型とエンドツーエンドの歌声合成システムの違いを理解できます。
- **代表的なモデル。** 主な研究目的ごとにモデルを探し、概要と利用可能な資料へのリンクを確認できます。
- **研究リソース。** 歌声データセット、コーパスの規模、およびアライメント、転写、分離、音声強調のツールを探せます。

## 目次

1. [はじめに](#introduction)
2. [全体構成](#overall)
3. [歌声合成のタスク](#tasks-of-svs)
4. [歌声合成システムの構成](#architectures-of-svs-systems)
5. [代表的なモデルと関連資料](#publicly-available-singing-voice-synthesis-models)
   - [2026年の主な研究（1〜10月）](#highlights-2026)
   - [歌声合成とボコーダ](#singing-synthesis-and-vocoders)
   - [スタイル制御と変換](#style-control-and-transfer)
   - [楽曲・音楽生成](#song-and-music-generation)
   - [関連する音声・歌声モデル](#related-speech-and-singing-models)
6. [リソース](#resources-in-svs-models)
   - [利用可能なデータセット](#open-source-datasets)
   - [アノテーションと前処理のツール](#annotation-tools-for-singing-data)
7. [引用](#citation)
8. [貢献方法](#contributing)
9. [ライセンス](#license)
10. [更新履歴](#update)

---

<a name="introduction"></a>

## 📌 はじめに

**Synthetic Singers** は、深層学習に基づく歌声合成のタスク、構成、モデル、データをまとめています。本リポジトリは[レビュー論文](https://aclanthology.org/2025.ijcnlp-long.24/)の関連資料として、研究者や実務者向けのガイドを提供します。

概要図ではレビューの構成と技術的な観点を示します。リソース表ではそれらを個々のプロジェクトと結び付け、関連システムの探索や歌声データの準備を支援します。

---

<a name="overall"></a>

## 🧭 全体構成

<div align="center">
  <img src="figure/organization.png" alt="Synthetic Singers のレビュー全体の構成" width="90%">
  <p><em>図 1. Synthetic Singers のレビュー全体の構成。</em></p>
</div>

---

<a name="tasks-of-svs"></a>

## 🎯 歌声合成のタスク

本レビューでは、歌声合成を四つのタスクに分類します。一つのシステムが複数のタスクに対応する場合もあります。

| タスク | 主な目的 | 確認すべき点 |
| --- | --- | --- |
| **高忠実度合成** | 歌詞と旋律に沿った、明瞭で自然な歌声を生成します。 | 音質、歌詞の明瞭さ、音程の正確さ。 |
| **制御可能な合成** | 合成品質を保ちながら歌唱の属性を調整します。 | 音色、スタイル、表現、歌唱技法の制御。 |
| **歌唱スタイル変換** | 参照する歌唱の声の特徴を再現します。 | 参照音声からの音色、スタイル、表現の引き継ぎ。 |
| **テキストからの楽曲生成** | テキスト入力から一つの楽曲を生成します。 | ボーカル、伴奏、楽曲構造の一貫性。 |

<div align="center">
  <img src="figure/tasks.png" alt="歌声合成タスクの概要" width="90%">
  <p><em>図 2. 歌声合成における四つの代表的なタスク。</em></p>
</div>

---

<a name="architectures-of-svs-systems"></a>

## 🏗️ 歌声合成システムの構成

波形生成に独立したボコーダを用いるかどうかによって、二つの構成方式に分類します。

| 方式 | 合成の流れ | 主な構成要素 |
| --- | --- | --- |
| **カスケード型歌声合成** | 音響特徴を予測し、その後に波形へ変換します。 | 音響モデルと独立したボコーダ。 |
| **エンドツーエンド歌声合成** | 統合された合成システム内で波形を生成します。 | 条件情報、中間表現、波形生成の共同モデリング。 |

<div align="center">
  <img src="figure/arch.png" alt="歌声合成システムの構成方式" width="90%">
  <p><em>図 3. カスケード型とエンドツーエンドの歌声合成構成。破線は任意の構成要素を示します。</em></p>
</div>

---

<a name="publicly-available-singing-voice-synthesis-models"></a>

## 📚 代表的なモデルと関連資料

モデルは主な研究目的ごとに分類し、機能が重なる場合があります。**Paper** は論文・プレプリント、**Code** は実装、**Model** は重みまたはダウンロード案内、**Demo** は例を示します。**Repo (planned)** は公開予定の公式リポジトリで、コード・重みの公開を意味しません。確認できた種類のリンクのみを掲載しており、リンクがないことは未公開の断定ではありません。非公式実装や **Model (TTS)** など用途が限られる版は明記しています。

<a name="highlights-2026"></a>

### 2026年の主な研究（1〜10月）

**収録範囲：2026-01-01〜2026-10-03。** 今回の追加12件は、楽譜に基づく歌声合成、発話・歌唱切り替え、歌詞編集、楽曲全体の生成を対象とします。年月は論文の初回公開時点であり、コード・重みの公開日とは限りません。会議名は正式な論文集に基づき、その他はプレプリントまたは技術報告です。旧論文の2026年改訂版は新規研究に数えません。

| 研究 | 初回論文／会議 | 研究内容 | リソース |
| --- | --- | --- | --- |
| HeartMuLa | 2026-01 · プレプリント／技術報告 | 歌詞・スタイル記述・参照音声を条件とする楽曲生成。低フレームレートの音楽コーデックを併用。 | [Paper](https://arxiv.org/abs/2601.10547v3) · [Code](https://github.com/HeartMuLa/heartlib) · [Model](https://huggingface.co/HeartMuLa/HeartMuLa-oss-3B-happy-new-year) |
| ACE-Step 1.5 | 2026-01 · プレプリント／技術報告 | 言語モデルによる楽曲設計と拡散生成を組み合わせ、編集と軽量な個別適応に対応。 | [Paper](https://arxiv.org/abs/2602.00744v3) · [Code](https://github.com/ace-step/ACE-Step-1.5) · [Model](https://huggingface.co/ACE-Step/Ace-Step1.5) |
| SoulX-Singer | 2026-02 · プレプリント／技術報告 | 楽譜または旋律を条件とするゼロショット歌声合成。普通話・英語・広東語に対応。 | [Paper](https://arxiv.org/abs/2602.07803v2) · [Code](https://github.com/Soul-AILab/SoulX-Singer) · [Model](https://huggingface.co/Soul-AILab/SoulX-Singer) |
| YingMusic-Singer / Plus | 2026-03 · Interspeech 2026 | 手動アラインメントを必要としない旋律保持型の歌詞編集。コードと重みは後続の Plus 版。 | [Paper](https://www.isca-archive.org/interspeech_2026/hao26_interspeech.html) · [Preprint](https://arxiv.org/abs/2603.24589) · [Code](https://github.com/ASLP-lab/YingMusic-Singer-Plus) · [Model](https://huggingface.co/ASLP-lab/YingMusic-Singer-Plus) |
| UniVocal | 2026-06 · ACL 2026 | テキストで制御する発話・歌唱の切り替え。公式リポジトリのコード・重み・SCSBench は公開予定。 | [Paper](https://aclanthology.org/2026.acl-long.1452/) · [Repo (planned)](https://github.com/QwenAudio/FunResearch/tree/main/UniVocal) · [Demo](https://project-univocal-demo.github.io/demo/) |
| UniVoice | 2026-06 · プレプリント／技術報告 | 内容・旋律・音色を別々の条件として扱う、音声と歌唱を統合したフローマッチング。 | [Paper](https://arxiv.org/abs/2606.05852v1) |
| MeloDISinger | 2026-06 · Interspeech 2026 | フローマッチングによる補完で歌詞を編集し、旋律・長さ・未編集部分を保持。 | [Paper](https://www.isca-archive.org/interspeech_2026/park26k_interspeech.html) · [Preprint](https://arxiv.org/abs/2606.30580v1) · [Demo](https://cottonlove.github.io/MeloDISinger_demo/) |
| LeVo 2 | 2026-06 · プレプリント／技術報告 | ボーカル・伴奏のストリームと拡散音楽コーデックを組み合わせた階層的楽曲モデリング。 | [Paper](https://arxiv.org/abs/2606.30642v1) · [Code](https://github.com/levo-demo/LeVo) · [Model](https://huggingface.co/lglg666/SongGeneration-v2-large) |
| Qwen-Music | 2026-07 · プレプリント／技術報告 | Melody-CoT による設計とフローマッチングによる音声生成で、楽曲生成とカバーに対応。 | [Paper](https://arxiv.org/abs/2607.11699v3) |
| VocalRender | 2026-07 · プレプリント／技術報告 | 歌詞・音高・音価・テンポを入力とする、自己回帰拡散による楽譜ベースの歌声合成。 | [Paper](https://arxiv.org/abs/2607.27768v1) · [Code](https://github.com/pymaster17/VocalRender) · [Model](https://huggingface.co/pymaster/VocalRender) · [Data](https://huggingface.co/datasets/pymaster/CrawlSinger-OS) |
| DiffSynth-Music | 2026-09 · プレプリント／技術報告 | ACE-Step を基盤とし、音声条件でビート・ボーカル・伴奏・韻律・参照音色を制御。 | [Paper](https://arxiv.org/abs/2609.12774v1) · [Code](https://github.com/modelscope/DiffSynth-Studio/tree/main/examples/diffsynth_music) · [Model](https://modelscope.cn/models/DiffSynth-Studio/DiffSynth-Music) |
| YuE2 | 2026-09 · プレプリント／技術報告 | 編集可能な旋律・コードを設計してから楽曲全体の音声を生成。ゼロショットのカバーにも対応。 | [Paper](https://arxiv.org/abs/2609.33757v1) · [Code](https://github.com/multimodal-art-projection/YuE) · [Model](https://huggingface.co/m-a-p/YuE2-3B) |

<a name="singing-synthesis-and-vocoders"></a>

### 歌声合成とボコーダ

| モデル | 研究の焦点 | リソース |
| --- | --- | --- |
| DiffSinger | 浅い拡散過程による歌声合成。 | [Paper](https://arxiv.org/abs/2105.02446) · [Code](https://github.com/MoonInTheRiver/DiffSinger) · [Model](https://github.com/MoonInTheRiver/DiffSinger/releases) |
| VISinger（非公式実装） | 変分推論と敵対的学習を用いたエンドツーエンド歌声合成。 | [Paper](https://arxiv.org/abs/2110.08813) · [Code](https://github.com/So-Fann/VISinger) |
| VISinger 2 | デジタル信号処理による合成器を組み込んだエンドツーエンド合成。 | [Paper](https://arxiv.org/abs/2211.02903) · [Code](https://github.com/zhangyongmao/VISinger2) · [Model](https://drive.google.com/file/d/1MgXLQuquPT2qu1__JNF010-tg48N0hZn/view) |
| VI-SVS | VITS に基づく歌声合成。 | [Code](https://github.com/PlayVoice/VI-SVS) · [Model](https://github.com/PlayVoice/VI-SVS/releases/tag/0.0.3) |
| NNSVS | ニューラル歌声合成の研究用ライブラリ。 | [Paper](https://arxiv.org/abs/2210.15987) · [Code](https://github.com/nnsvs/nnsvs) |
| CoMoSpeech | 一貫性モデルによる一段階の音声・歌声合成。 | [Paper](https://arxiv.org/abs/2305.06908) · [Code](https://github.com/zhenye234/CoMoSpeech) · [Model (TTS)](https://drive.google.com/drive/folders/1rkbzl9NzS_fKtMubQ7FgSdgt7v8ZuYGk) |
| HiFiSinger | 高忠実度のニューラル歌声合成。リンク先は Muzic の研究概要です。 | [Paper](https://arxiv.org/abs/2009.01776) · [Overview](https://github.com/microsoft/muzic) |
| HiFiSinger（非公式実装） | HiFiSinger の独立した再実装。 | [Paper](https://arxiv.org/abs/2009.01776) · [Code](https://github.com/CODEJIN/HiFiSinger) |
| ByteSing | 長さのモデリングと WaveRNN ボコーダによる中国語歌声合成。 | [Paper](https://arxiv.org/abs/2004.11012) |
| WeSinger | データ拡張と補助損失を用いた歌声合成。 | [Paper](https://arxiv.org/abs/2203.10750) · [Demo](https://zzw922cn.github.io/wesinger/) |
| SingGAN | 高忠実度の歌声を実現する敵対的な波形生成。 | [Paper](https://arxiv.org/abs/2110.07468) · [Demo](https://singgan.github.io/) |
| UniSinger | モダリティ間の情報マッチングによる統合的なエンドツーエンド歌声合成。 | [Paper](https://doi.org/10.1145/3581783.3612150) · [Repo (planned)](https://github.com/ViEm-ccy/UniSinger) · [Demo](https://unisinger.github.io/Samples/) |
| Learn2Sing 2.0 | 歌唱者の歌声から学習し、対象話者の歌声を合成。 | [Paper](https://arxiv.org/abs/2203.16408) · [Code](https://github.com/WelkinYang/Learn2Sing2.0) · [Demo](https://welkinyang.github.io/Learn2Sing2.0/) |
| UniSyn | テキスト音声合成と歌声合成を統合したエンドツーエンドモデル。 | [Paper](https://arxiv.org/abs/2212.01546) |

<a name="style-control-and-transfer"></a>

### スタイル制御と変換

| モデル | 研究の焦点 | リソース |
| --- | --- | --- |
| StyleSinger | 学習ドメイン外の歌声に対するスタイル変換。 | [Paper](https://arxiv.org/abs/2312.10741) · [Code](https://github.com/AaronZ345/StyleSinger) · [Model](https://huggingface.co/AaronZ345/StyleSinger) |
| TCSinger | スタイル変換と多段階の制御に対応したゼロショット歌声合成。 | [Paper](https://aclanthology.org/2024.emnlp-main.117/) · [Code](https://github.com/AaronZ345/TCSinger) · [Model](https://huggingface.co/AaronZ345/TCSinger) |
| TCSinger 2 | カスタマイズ可能な多言語ゼロショット歌声合成。 | [Paper](https://arxiv.org/abs/2505.14910) · [Code](https://github.com/AaronZ345/TCSinger2) |
| FreeStyler | ラップ生成。リンク先の RapBank はデータと処理ツールを提供します。 | [Paper](https://arxiv.org/abs/2408.15474) · [Code (data)](https://github.com/NZqian/RapBank) · [Demo](https://nzqian.github.io/Freestyler/) |
| AlignSTS | モダリティ間のアライメントによる話し声から歌声への変換。 | [Paper](https://arxiv.org/abs/2305.04476) · [Code](https://github.com/RickyL-2000/AlignSTS) · [Model](https://drive.google.com/file/d/1hKesxqkbrBKC06eYLmlCutPathdJLCK1/view) |
| ExpressiveSinger | 多言語・多様なスタイルの歌唱における表現制御。 | [Paper](https://doi.org/10.1145/3664647.3681642) · [Demo](https://expressivesinger.github.io/ExpressiveSinger/) |
| TechSinger | フローマッチングによる多言語の歌唱技法制御。 | [Paper](https://arxiv.org/abs/2502.12572) · [Code](https://github.com/gwx314/TechSinger) · [Model](https://huggingface.co/verstar/TechSinger) |
| Prompt-Singer | 自然言語プロンプトによる歌声合成の制御。 | [Paper](https://arxiv.org/abs/2403.11780) · [Code](https://github.com/cyanbx/Prompt-Singer) · [Model](https://huggingface.co/Cyanbox/Prompt-Singer) |

<a name="song-and-music-generation"></a>

### 楽曲・音楽生成

| モデル | 研究の焦点 | リソース |
| --- | --- | --- |
| YuE | 歌詞からの楽曲生成。リンク先のブランチは初代 YuE のリリースを保持しています。 | [Paper](https://arxiv.org/abs/2503.08638) · [Code](https://github.com/multimodal-art-projection/YuE/tree/YuE-v1) · [Model](https://huggingface.co/m-a-p/YuE-s1-7B-anneal-en-cot) |
| InspireMusic | 音楽、楽曲、音声の生成用ツールキット。 | [Paper](https://arxiv.org/abs/2503.00084) · [Code](https://github.com/FunAudioLLM/InspireMusic) · [Model (music)](https://modelscope.cn/models/iic/InspireMusic-1.5B-Long) |
| SongGen | 単一段階の自己回帰 Transformer によるテキストからの楽曲生成。 | [Paper](https://arxiv.org/abs/2502.13128) · [Code](https://github.com/LiuZH-19/SongGen) · [Model](https://huggingface.co/LiuZH-19/SongGen_mixed_pro) |
| DiffRhythm | 潜在拡散によるエンドツーエンドのフルレングス楽曲生成。 | [Paper](https://arxiv.org/abs/2503.01183) · [Code](https://github.com/ASLP-lab/DiffRhythm) · [Model](https://huggingface.co/ASLP-lab/DiffRhythm-full) |
| Levo | ボーカルと伴奏を含む楽曲生成。 | [Paper](https://arxiv.org/abs/2506.07520) · [Code](https://github.com/levo-demo/LeVo) · [Model](https://huggingface.co/lglg666/SongGeneration-base-new) |

<a name="related-speech-and-singing-models"></a>

### 関連する音声・歌声モデル

| モデル | 研究の焦点 | リソース |
| --- | --- | --- |
| NaturalSpeech 2（非公式実装） | 拡散モデルによる音声・歌声合成。リンク先は非公式実装です。 | [Paper](https://arxiv.org/abs/2304.09116) · [Code](https://github.com/lucidrains/naturalspeech2-pytorch) |
| SpeechGPT-Gen | 情報連鎖のモデリングによる音声生成。 | [Paper](https://arxiv.org/abs/2401.13527) · [Repo (planned)](https://github.com/0nutation/SpeechGPT/tree/main/speechgpt-gen) · [Demo](https://0nutation.github.io/SpeechGPT-Gen.github.io/) |

---

<a name="resources-in-svs-models"></a>

## 📦 リソース

この節では、学習・評価データの準備に役立つ歌声データセットとツールをまとめます。

<a name="open-source-datasets"></a>

### 📊 利用可能なデータセット

**データセットと付属資料45件**を収録し、歌声合成の学習、整列・採譜、分離、評価を対象とします。**Data** は公開データ、**Annotations / Metadata** は注釈・出典一覧、**Access** は申請が必要な場合もある取得案内です。論文のみ、または公開予定の項目は明記しています。言語コード：zh = 普通話、en = 英語、ja = 日本語、ko = 韓国語。その他の多言語資料は確認できる場合に言語数を記載しています。

既存コーパスの統計は[サーベイ表1](https://arxiv.org/html/2601.13910v1)を出発点とし、著者の公開資料とデータ論文に基づいて版の情報と統計を補正しています。長さは概数です。ACE の時間は**コーパス全体の合計**で、音色数は合成音色を指します。派生コーパスと評価用サブセットは重複するため、各行の単純な合計を固有音声の総量にはできません。

[歌唱・SVS 学習コーパス](#svs-training-corpora) · [歌詞・音符・楽曲構造・分離データ](#alignment-and-separation-data) · [評価ベンチマークと付属注釈](#singing-evaluation-benchmarks)

<a name="svs-training-corpora"></a>

#### 歌唱・SVS 学習コーパス

| データセット | 言語／規模 | 内容と提供状況 | リソース |
| --- | --- | --- | --- |
| NUS-48E | en · 歌手 12人 | 歌唱115分＋発話54分、音素境界付き。論文にコーパス情報を掲載。 | [Paper](https://ieeexplore.ieee.org/document/6694316) |
| VocalSet | en · 歌手 20人 · 10.1 h | さまざまな音高・文脈で収録した歌唱技法と母音。 | [Data](https://zenodo.org/records/1203819) |
| CSD | ko / en · 100曲 | 歌手1人、各曲2調で計200録音。MIDI と音素・文字単位の歌詞を収録。 | [Code](https://github.com/emotiontts/emotiontts_open_db/tree/master/Dataset/CSD) · [Data](https://zenodo.org/records/4785016) |
| PJS | ja · 歌手 1人 · 0.5 h | 音素バランスを考慮した日本語歌唱と楽譜・時間情報。 | [Paper](https://arxiv.org/abs/2006.02959) · [Data](https://sites.google.com/site/shinnosuketakamichi/research-topics/pjs_corpus) |
| NHSS | en · 歌手 10人 · 7 h | 100曲の並列発話・歌唱を含む合計時間。利用申請書とメールでの申請が必要。 | [Paper](https://arxiv.org/abs/2012.00337) · [Access](https://hltnus.github.io/NHSSDatabase/download.html) |
| OpenSinger | zh · 歌手 66人 · 50 h | 歌声合成・声質変換向けの複数歌手による中国語録音。 | [Access](https://multi-singer.github.io/) |
| Tohoku Kiritan | ja · 50曲 | 単一歌手の録音と楽譜資料。提供元の利用手続きに従って取得。 | [Access](https://zunko.jp/kiridev/login.php) |
| PopCS | zh · 歌手 1人 · 5.9 h | DiffSinger の中国語コーパス。申請による提供。 | [Paper](https://arxiv.org/abs/2105.02446) · [Access](https://github.com/MoonInTheRiver/DiffSinger/blob/master/resources/apply_form.md) |
| M4Singer | zh · 歌手 20人 · 29.8 h | 手作業の楽譜・歌詞・音素注釈。ソプラノ、アルト、テノール、バスを収録。 | [Code](https://github.com/M4Singer/M4Singer) · [Data](https://drive.google.com/file/d/1xC37E59EWRRFFLdG3aJkVqwtLDgtFNqW/view) |
| PopBuTFy | zh / en · 歌手 34人 · 50.8 h | 歌唱補正向けのアマチュア・プロの録音。利用案内は NeuralSVB を参照。 | [Paper](https://arxiv.org/abs/2202.13277) · [Code / Access](https://github.com/MoonInTheRiver/NeuralSVB) |
| Opencpop | zh · 歌手 1人 · 5.2 h | 音素・音符境界付きの中国語ポップス歌唱。フォーム送信後にメールで取得案内。 | [Paper](https://arxiv.org/abs/2201.07429) · [Access](https://wenet-e2e.github.io/opencpop/download/) |
| SingStyle111 | 3 言語 · 歌手 8人 · 12.8 h | 多言語の歌唱スタイルコーパス。Zenodo でアクセス制限あり。 | [Access](https://zenodo.org/records/10265401) |
| GTSinger | 9 言語 · 歌手 20人 · 80.6 h | 歌唱技法ラベル付きの多言語歌唱、対応する発話と楽譜注釈。 | [Paper](https://arxiv.org/abs/2409.13832) · [Code](https://github.com/GTSinger/GTSinger) · [Data](https://huggingface.co/datasets/AaronZ345/GTSinger) |
| ACE-Opencpop | zh · 30 音色 · 128.9 h | 30人の実歌手ではなく合成音色。合計128.9 h、1音色あたり平均4.3 h。 | [Paper](https://arxiv.org/abs/2401.17619v2) · [Data](https://huggingface.co/datasets/espnet/ace-opencpop-segments) |
| ACE-KiSing | zh / en · 34 音色 · 32.5 h | 合成歌唱によるデータ拡張。合計32.5 h、1音色あたり約1 h。 | [Paper](https://arxiv.org/abs/2401.17619v2) · [Data](https://huggingface.co/datasets/espnet/ace-kising-segments) |
| KiSing-v1 | zh · 歌手 1人 · 0.7 h | 14曲の元の実録音コーパス。合成の ACE-KiSing とは別で、参考論文に両者の説明あり。 | [Reference](https://arxiv.org/abs/2401.17619v2) |
| JVS-MuSiC | ja · 歌手 100人 · 2.3 h | 各歌手2曲。関連する JVS の朗読コーパスと組み合わせて利用可能。 | [Paper](https://arxiv.org/abs/2001.07044) · [Data](https://sites.google.com/site/shinnosuketakamichi/research-topics/jvs_music) |
| JSUT-song | ja · 27曲 | 単一歌手の童謡と楽譜・音素アラインメント資料。 | [Data](https://sites.google.com/site/shinnosuketakamichi/publication/jsut-song) |
| NIT-SONG070-F001 | ja · 31曲 | HTS/Sinsy 研究で使用される日本語の単一歌手コーパス。比較文献を参照。 | [Reference](https://arxiv.org/abs/2401.17619v2) |
| CrawlSinger-OS | zh · 2,317 h · 776k セグメント | 合成・実録音を含み、歌詞・音高・音価・テンポを付与。他の掲載コーパスと出典が重複。 | [Paper](https://arxiv.org/abs/2607.27768v1) · [Code](https://github.com/pymaster17/VocalRender) · [Data](https://huggingface.co/datasets/pymaster/CrawlSinger-OS) |
| OpenSongSong | zh · 29.9 h | SongSong（AAAI 2025）の宋詞歌唱コーパス。ダウンロード可能な公開版は未確認。 | [Paper](https://ojs.aaai.org/index.php/AAAI/article/view/34820) · [Demo](https://zcli-charlie.github.io/projects/songsong/) |
| SingNet | 多言語 · ~3,000 h | 論文で紹介された実環境の歌唱コーパスと処理工程。公開音声のダウンロードは未確認。 | [Paper](https://arxiv.org/abs/2505.09325) |

<a name="alignment-and-separation-data"></a>

#### 歌詞・音符・楽曲構造・分離データ

| データセット | 言語／規模 | 内容と提供状況 | リソース |
| --- | --- | --- | --- |
| KVT | ko · 歌手 114人 · 18.9 h | 歌声音色・スタイルのタグ。論文では注釈と出典リンクを説明し、音声は再配布しない。 | [Paper](https://ieeexplore.ieee.org/document/9097399) |
| MIR-1K | zh · 歌手 19人 · 2.2 h | 歌声分離・音高研究向けのボーカル／伴奏の抜粋1,000件。 | [Data](https://zenodo.org/records/3532216) |
| DAMP-MVP / Sing! 300×30×2 | 多言語 | カラオケ歌唱・歌詞・メタデータ。音声へのアクセスには許可が必要。 | [Access](https://zenodo.org/records/2747436) |
| DSing | en · DAMP サブセット | 歌詞文字起こし用の分割と実験レシピ。元音声は DAMP で利用申請。 | [Code / Annotations](https://github.com/groadabike/Kaldi-Dsing-task) · [Access](https://zenodo.org/records/2747436) |
| DALI | 多言語 (v1) · 5358曲 | 整列済みの歌詞・歌唱音符。音声一式ではなく、注釈と音声取得コードを提供。 | [Paper](https://arxiv.org/abs/1906.10606) · [Code / Annotations](https://github.com/gabolsgabs/DALI) |
| RapBank | 84 言語 · 5,586 h （収集規模） | ラップ動画IDと処理工程。報告された収集規模は、配布音声の容量を表すものではない。 | [Paper](https://arxiv.org/abs/2408.15474) · [Code / Metadata](https://github.com/NZqian/RapBank) |
| MIR-ST500 | ポップス · 500曲 | 歌唱音符注釈と元URLを提供。著作権で保護された音声は再配布しない。 | [Paper](https://ieeexplore.ieee.org/document/9414601) · [Code / Annotations](https://github.com/york135/singing_transcription_ICASSP2021) |
| JamendoLyrics MultiLang | en / fr / de / es · 79曲 | 単語・行単位の歌詞時刻付き音声。現行の Hugging Face 公開版。 | [Paper](https://arxiv.org/abs/2306.07744) · [Data](https://huggingface.co/datasets/jamendolyrics/jamendolyrics) |
| MuChin 1k / v2-6066 | zh (v2) · 6066曲 | 音楽記述・構造・歌詞。v2 の重複注釈と歌詞時刻に関する案内を確認。 | [Paper](https://www.ijcai.org/proceedings/2024/0860.pdf) · [Code](https://github.com/CarlWangChina/MuChin-V2-6066) · [Data](https://huggingface.co/datasets/karl-wang/MuChin-v2-6066) |
| SongFormDB | 多言語 · >10k 曲 | 4サブセットの楽曲構造ラベル。音声の復元手順は出典ごとに指定。 | [Paper](https://arxiv.org/abs/2510.02797) · [Data](https://huggingface.co/datasets/ASLP-lab/SongFormDB) |
| MUSDB18 / MUSDB18-HQ | 多言語 · 150曲 | 約10 h。ボーカル・ベース・ドラム・その他のステム。HQ は同じ楽曲の高音質版。 | [Access](https://sigsep.github.io/datasets/musdb.html) · [Data (HQ)](https://zenodo.org/records/3338373) |
| DSD100 | 多言語 · 100曲 | ボーカル・伴奏分離用ステム。MUSDB18 にも収録。 | [Data](https://sigsep.github.io/datasets/dsd100.html) |
| MedleyDB 1.0 / 2.0 | 122 + 74 曲のマルチトラック録音 | 楽器・ボーカルのステムと旋律注釈。器楽曲も含み、音声は申請制。 | [Access / Annotations](https://medleydb.weebly.com/) |
| jaCappella v2 | ja · 50曲 | 各曲6声部の独立音源と PDF/MusicXML 楽譜。提供元の利用規約を適用。 | [Paper](https://arxiv.org/abs/2211.16028) · [Data](https://huggingface.co/datasets/jaCappella/jaCappella) |

<a name="singing-evaluation-benchmarks"></a>

#### 評価ベンチマークと付属注釈

| データセット | 言語／規模 | 内容と提供状況 | リソース |
| --- | --- | --- | --- |
| Annotated-VocalSet | VocalSet 付属資料 | VocalSet の追加注釈。独立した音声コーパスとして重複計上しない。 | [Annotations](https://zenodo.org/records/7061507) |
| SoulX-Singer-Eval | zh / en · 100 クリップ · 50 人の歌手 | ドメインをまたぐゼロショット歌声評価。同じ公開先に GMO-SVS の802サンプルも収録。 | [Paper](https://arxiv.org/abs/2602.07803v2) · [Code](https://github.com/Soul-AILab/SoulX-Singer-Eval) · [Data](https://huggingface.co/datasets/Soul-AILab/SoulX-Singer-Eval-Dataset) |
| LyricEditBench | zh / en · 7,200 件 | GTSinger 由来の旋律保持型歌詞編集6課題。元の録音と重複。 | [Paper](https://arxiv.org/abs/2603.24589) · [Code](https://github.com/ASLP-lab/YingMusic-Singer-Plus) · [Data](https://huggingface.co/datasets/ASLP-lab/LyricEditBench) |
| SCSBench | UniVocal · ACL 2026 | 発話・歌唱切り替えベンチマーク。論文で紹介済みだが、公式データは公開予定。 | [Paper](https://aclanthology.org/2026.acl-long.1452/) · [Repo (planned)](https://github.com/QwenAudio/FunResearch/tree/main/UniVocal) |
| MMGenre | zh · 3,152 ペア · 4.36 h | 合成歌唱と楽譜のペア。公開カードでは148曲、10ジャンル・26サブジャンル。 | [Paper](https://arxiv.org/abs/2607.06986) · [Code](https://github.com/FengJin1117/mmgenre) · [Data](https://huggingface.co/datasets/Leaky-ReLU/MMGenre) |
| WildSongBench | zh / en · 192 プロンプト | 楽曲生成のプロンプト・乱数シード・評価ツール。参照音声は含まない。 | [Paper](https://arxiv.org/abs/2609.33757v1) · [Data (prompts)](https://huggingface.co/datasets/m-a-p/WildSongBench) |
| SingMOS / SingMOS-Pro | 主観品質評価 | 人手の品質評価付き歌声サンプル。MOS 予測と評価に利用。 | [Paper](https://arxiv.org/abs/2406.10911) · [Paper (Pro)](https://arxiv.org/abs/2510.01812) · [Code](https://github.com/South-Twilight/SingMOS) · [Data](https://huggingface.co/datasets/TangRain/SingMOS-v1) · [Data (Pro)](https://huggingface.co/datasets/TangRain/SingMOS-Pro) |
| SingFox | 20 言語 · 113,802 クリップ · 126.32 h | 歌唱ディープフェイク検出・生成元追跡（Interspeech 2026）。構築コードは公開、全音声の公開版は未確認。 | [Paper](https://www.isca-archive.org/interspeech_2026/shah26_interspeech.html) · [Code](https://github.com/Arth-Shah/SingFox) |
| Jam-ALT | en / fr / de / es · 79曲 | 歌詞を修訂し行時刻を付けた文字起こしベンチマーク。音声は JamendoLyrics と同一。 | [Paper](https://arxiv.org/abs/2408.06370) · [Code](https://github.com/audioshake/alt-eval) · [Data](https://huggingface.co/datasets/jamendolyrics/jam-alt) |

<a name="annotation-tools-for-singing-data"></a>

### 🛠️ アノテーションと前処理のツール

以下のリソースは、歌詞のアライメント、歌声の音符転写、よりクリーンなボーカル音源の準備に利用できます。

| ツール | タスク | リソース |
| --- | --- | --- |
| MFA | 音声とテキストの強制アライメント | [Paper](https://doi.org/10.21437/Interspeech.2017-1386) · [Code](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner) |
| SOFA | 歌声とテキストの強制アライメント | [Code](https://github.com/qiuqiao/SOFA) · [Model (community)](https://github.com/qiuqiao/SOFA/discussions/categories/pretrained-model-sharing) |
| VOCANO | 歌声の音符転写 | [Paper](https://archives.ismir.net/ismir2021/paper/000036.pdf) · [Code](https://github.com/B05901022/VOCANO) |
| MusicYOLO | 音楽の音符転写 | [Code](https://github.com/itec-hust/MusicYOLO) · [Model](https://pan.baidu.com/s/1TbE36ydi-6EZXwxo5DwfLg?pwd=1234) |
| ROSVOT | 歌声の音符転写 | [Paper](https://arxiv.org/abs/2405.09940) · [Code](https://github.com/RickyL-2000/ROSVOT) · [Model](https://drive.google.com/file/d/1JNtNT37KiLq9uFQqHk7JFs-3trxd3bRh/view) |
| STARS | 統合アノテーションモデル | [Paper](https://arxiv.org/abs/2507.06670) · [Code](https://github.com/gwx314/STARS) · [Model](https://huggingface.co/verstar/STARS) |
| UVR | ボーカルと伴奏の分離 | [Code](https://github.com/Anjok07/ultimatevocalremovergui) · [App](https://ultimatevocalremover.com/) |
| ClearerVoice | 音声強調 | [Paper](https://arxiv.org/abs/2506.19398) · [Code](https://github.com/modelscope/ClearerVoice-Studio) · [Model](https://modelscope.cn/models/iic/ClearerVoice-Studio) |
| SheetSage2 | ボーカル旋律とコードのリードシート採譜。技術報告の公開日：2026-10-02。 | [Report](https://github.com/multimodal-art-projection/YuE/blob/main/docs/sheetsage2_technical_report.pdf) · [Code / Model](https://huggingface.co/m-a-p/SheetSage2) |

---

<a name="citation"></a>

## 📝 引用

本リポジトリが研究に役立った場合は、IJCNLP-AACL 2025 に掲載された論文をご引用ください。

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

## 🤝 貢献方法

資料の追加や誤りの修正を歓迎します。論文、モデル、データセット、ツールを提案する場合は、名称、一次情報へのリンク、歌声合成との関連を示す簡単な説明を添えて、[Issue](https://github.com/DaViD-Pigeon/SyntheticSingers/issues) または Pull Request を送ってください。非公式実装にはその旨を記載し、コード、モデル重み、データセット、デモを区別してください。

---

<a name="license"></a>

## 📄 ライセンス

本リポジトリ向けに作成したオリジナルの文書には [MIT ライセンス](LICENSE) が適用されます。レビュー論文、論文から転載した図、およびリンク先の第三者の論文、コード、モデル重み、データセット、ツールには、それぞれのライセンスが適用されます。

---

<a name="update"></a>

## 🔄 更新履歴

**本リポジトリは毎月少なくとも一度、内容の追加と更新を行います。** 関連する論文、モデル、データセット、ツールを追加し、情報を修正するとともに、更新内容をここに記録します。

- **2026-10-03**：README の構成とナビゲーションを整え、中国語・韓国語・日本語版を追加。2026年の代表的なモデル論文12件と SheetSage2 ツールを追加し、データセット・付属資料を45件に拡充。Paper / Code / Model リンクと公開状況を確認して統計を修正し、貢献案内・ライセンス・月次更新記録を整備しました。
- **2026-01**: Synthetic Singers のレビューを [arXiv](https://arxiv.org/abs/2601.13910v1) で公開し、モデル、データセット、アノテーションツールをまとめた関連リポジトリを公開しました。
