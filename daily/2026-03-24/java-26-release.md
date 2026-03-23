# Java 26 リリースの注目機能

- **日付**: 2026-03-24
- **カテゴリ**: Tech
- **ソース**: [InfoQ](https://www.infoq.com/news/2026/03/java26-released/), [OpenJDK](https://openjdk.org/projects/jdk/26/), [Oracle Blog](https://blogs.oracle.com/java/the-arrival-of-java-26)

## 概要

Oracle は2026年3月17日に Java 26（JDK 26）をリリースした。JDK 25（LTS）以来初の非LTSリリースで、10の JEP（Java Enhancement Proposal）を含む。言語改善、ライブラリ強化、パフォーマンス向上、セキュリティ強化の4つの柱に注力しており、AI 推論ワークロードの効率化を意識した改善も含まれている。

## 詳細

### 言語機能

**JEP 530: Primitive Types in Patterns, instanceof, and switch（第4プレビュー）**

パターンマッチング、instanceof、switch でのプリミティブ型の制限を撤廃し、Java をより統一的かつ表現力豊かにする。AI 推論を統合するアプリケーション開発の効率化にも寄与する。第4プレビューであり、正式化に向けた最終段階に入っている。

### パフォーマンス改善

**JEP 516: Ahead-of-Time Object Caching**

HotSpot JVM の AOT キャッシュを拡張し、ZGC を含むすべての GC でキャッシュ済み Java オブジェクトを利用可能に。GC 非依存のフォーマットでオブジェクトを保存し、起動時にシーケンシャルにメモリへロードすることで、起動時間を大幅に短縮する。

**JEP 522: G1 GC — Improve Throughput by Reducing Synchronization**

G1 ガベージコレクタにおけるアプリケーションスレッドと GC スレッド間の同期を削減し、スループットを向上。メモリ効率の改善により、より多くのワークロードを短時間で処理可能にする。

### ライブラリ・API

**HTTP/3 for the HTTP Client API**

Java の HTTP Client API が HTTP/3（QUIC ベース）をサポート。モダンなネットワーク通信に対応し、レイテンシ削減とコネクション確立の高速化を実現。

**Lazy Constants（第2プレビュー）**

遅延初期化される定数を言語レベルでサポートし、不要な初期化コストを回避。

**Structured Concurrency（第6プレビュー）**

構造化並行処理の6度目のプレビュー。長いプレビュー期間を経て、API の安定化が進んでいる。

**Vector API（第11インキュベーション）**

SIMD 演算を Java から直接利用するための API。11回目のインキュベーションであり、Project Panama の一環として段階的に進化を続けている。

### セキュリティ

**Prepare to Make Final Mean Final**

ディープリフレクションによる final フィールドの変更時に警告を出力。将来のリリースで final を本当に不変にするための準備段階であり、プログラムの安全性と潜在的な最適化の余地を向上させる。

**PEM Encodings of Cryptographic Objects（第2プレビュー）**

暗号オブジェクトの PEM（Privacy-Enhanced Mail）エンコーディングをサポートし、証明書や鍵の扱いを簡素化。

### Applet API の削除

Java Applet API が正式に削除された。長年非推奨であったブラウザプラグイン関連の API がついに完全に除去され、プラットフォームの簡素化が進んだ。

## 今後の注目点

- JDK 27（2025年9月予定）での Primitive Types in Patterns の正式化の可能性
- Structured Concurrency の正式版入り — 6回のプレビューを経て次のリリースで GA になるか
- Vector API のインキュベーション卒業時期 — Project Valhalla との統合が鍵
- AI/ML ワークロード向けの最適化が Java エコシステムにどこまで浸透するか
- IntelliJ IDEA 等の主要 IDE による Java 26 サポート状況（JetBrains は[リリース同日にサポートを発表](https://blog.jetbrains.com/idea/2026/03/java-26-in-intellij-idea/)）
