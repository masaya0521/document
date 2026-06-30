# Qualcomm による Tenstorrent 買収交渉 — RISC-V でデータセンター AI へ

- **日付**: 2026-07-01
- **カテゴリ**: Tech
- **ソース**: [The Register](https://www.theregister.com/systems/2026/06/16/qualcomm-said-to-be-circling-ai-chip-biz-tenstorrent-in-10b-risc-v-power-play/) / [AI Weekly](https://aiweekly.co/alerts/qualcomm-targets-tenstorrent-in-reported-10b-risc-v-deal)

## 概要

Qualcomm が、伝説的チップアーキテクト Jim Keller 率いる RISC-V ベースの AI チップスタートアップ **Tenstorrent** を **80〜100億ドル**で買収する協議に入っていると報じられた（2026年6月15日報道、Reuters も同日確認）。実現すれば AI ハードウェア分野で過去最大級の買収の一つとなる。Tenstorrent の評価額は直近の約32億ドルから約1年で **2.5〜3倍** に跳ね上がった計算になる。

Qualcomm はモバイル・エッジ向け SoC で圧倒的な地位を持つが、急成長するデータセンター AI 市場では存在感が薄い。本買収は、NVIDIA / AMD が支配する AI アクセラレータ市場へ「オープンな RISC-V スタック」で切り込む布石と位置づけられる。

## 詳細

### 戦略的な意味

買収が完了すれば、Qualcomm は **データセンター向けの RISC-V AI アクセラレータのフルスタック**を一気に手に入れる。これは、プロプライエタリな命令セット（NVIDIA の CUDA エコシステムや x86 依存）に対する「オープン標準による対抗軸」を強化する動きだ。Tenstorrent は RISC-V という業界標準を採用しており、Qualcomm にとっては自社の命令セット戦略とも整合性が高い。

### 一連の RISC-V 買収の総仕上げ

今回の交渉は単発ではなく、Qualcomm が継続してきた RISC-V・サーバー領域への投資の延長線上にある。

- **2025年12月**: RISC-V サーバー CPU スタートアップ **Ventana Micro Systems** を買収
- **同時期**: **Alphawave Semi** を24億ドルで買収完了（高速 SerDes / チップレット接続 IP）
- **2026年6月**: Tenstorrent 買収交渉が表面化

これらを束ねると、「CPU（Ventana）＋ AI アクセラレータ（Tenstorrent）＋ 高速インターコネクト（Alphawave）」というデータセンター AI の主要構成要素を揃える絵が見えてくる。

### 競合の動き

Tenstorrent には **Intel も関心を示している**とされ、競争入札の様相を呈している。Intel 自身も自社 AI アクセラレータ戦略に苦戦しており、Jim Keller の設計資産は両社にとって魅力的だ。なお交渉は進行中で、成立の保証はない。

## 今後の注目点

- **成約の有無と最終価格**: $8〜10B のレンジで決着するか、Intel との競合で吊り上がるか。
- **RISC-V の AI 採用加速**: 大手による買収は、データセンター AI における RISC-V の正当性を一段押し上げる可能性。OSS / オープン標準コミュニティへの波及を注視。
- **NVIDIA 一強への対抗構図**: Qualcomm + Tenstorrent が CUDA エコシステムにどこまで対抗できるか。オープンコンパイラ / ソフトウェアスタックの成熟度が鍵。
- **規制当局の審査**: 大型半導体 M&A は各国の独禁当局審査の対象になりやすく、承認プロセスが長期化するリスク。
- **Jim Keller の去就**: 設計の中核人物が買収後も残るかどうかが、技術的価値の維持を左右する。
