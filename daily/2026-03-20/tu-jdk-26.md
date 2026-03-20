# JDK 26 GA — 10個のJEPで進化するJava

- **日付**: 2026-03-17
- **カテゴリ**: Language
- **ソース**: [Oracle Blog](https://blogs.oracle.com/java/the-arrival-of-java-26), [InfoQ](https://www.infoq.com/news/2026/03/java26-released/), [OpenJDK](https://openjdk.org/projects/jdk/26/)

## 概要

JDK 26 が 2026年3月17日に General Availability を迎えた。JDK 25（LTS）以来初の非LTSリリースで、10個のJEP（Java Enhancement Proposal）を含む。ライブラリ改善、言語革新、パフォーマンス、セキュリティの4領域にわたる機能強化が行われている。Oracle は AI ワークロードへの対応として5つの機能（プリミティブ型パターン、Vector API、構造化並行性、Lazy Constants、AOTオブジェクトキャッシング）を特に強調している。

## 主な変更点

### 確定機能（5 JEP）

| JEP | 内容 |
|-----|------|
| JEP 500 | final フィールドの deep reflection による変更に対する警告の導入 |
| JEP 504 | Applet API の完全削除 |
| JEP 516 | 全GCでの AOT オブジェクトキャッシング |
| JEP 517 | HTTP クライアント API での HTTP/3 サポート |
| JEP 522 | G1 GC の同期削減によるスループット改善 |

### プレビュー / インキュベータ機能（5 JEP）

| JEP | 内容 | ステージ |
|-----|------|---------|
| JEP 524 | 暗号オブジェクトの PEM エンコーディング | 第2プレビュー |
| JEP 525 | 構造化並行性（Structured Concurrency） | 第6プレビュー |
| JEP 526 | Lazy Constants | 第2プレビュー |
| JEP 529 | Vector API | 第11インキュベータ |
| JEP 530 | パターン・instanceof・switch でのプリミティブ型 | 第4プレビュー |

### パフォーマンス改善

- **AOT オブジェクトキャッシング（JEP 516）**: JDK 24 で導入された AOT クラスローディング機能を拡張。低レイテンシー Z Garbage Collector を含む任意の GC で利用可能に。起動時間とウォームアップの短縮に寄与
- **G1 GC スループット改善（JEP 522）**: G1 ガベージコレクタの同期処理を削減し、スループットを向上

### セキュリティ強化

- **HTTP/3 サポート（JEP 517）**: HTTP クライアント API が HTTP/3 プロトコルに対応
- **PEM エンコーディング（JEP 524）**: PKCS #8 および X.509 バイナリフォーマット間の変換をサポートする暗号化 API の強化

## 破壊的変更

- **Applet API の削除（JEP 504）**: JDK 9 での非推奨化、JDK 17 での削除予告を経て、Applet API が完全に削除された。Web ブラウザがアプレットをサポートしなくなったことが背景
- **final フィールド変更への警告（JEP 500）**: deep reflection を使用して final フィールドを変更するコードに対して警告が出るようになった。将来的にはエラーに昇格する可能性がある

## 今後の注目点

- 構造化並行性（第6プレビュー）と Vector API（第11インキュベータ）が今後の安定化に向けてどのように進むか
- JDK 27 に向けたプリミティブ型パターンの正式化の行方
- AI / ML ワークロード向け機能（Vector API、AOT キャッシング）の実用性の評価
- 次の LTS リリース（JDK 29 予定）までのロードマップ
