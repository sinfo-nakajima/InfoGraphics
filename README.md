# InfoGraphics

GitHubのMarkdownファイル（`.md`）に各種の図形を表示する方法を紹介します。

---

## 目次

1. [Mermaid ダイアグラム](#1-mermaid-ダイアグラム)
   - [フローチャート](#フローチャート)
   - [シーケンス図](#シーケンス図)
   - [クラス図](#クラス図)
   - [ガントチャート](#ガントチャート)
   - [円グラフ](#円グラフ)
   - [ER図](#er図)
2. [SVG 画像](#2-svg-画像)
3. [HTMLテーブルによるビジュアル表現](#3-htmlテーブルによるビジュアル表現)
4. [テキストアート（AAアート）](#4-テキストアートaaアート)
5. [まとめ](#5-まとめ)

---

## 1. Mermaid ダイアグラム

GitHub は 2022年より Mermaid ダイアグラムをネイティブサポートしています。  
コードブロックの言語指定を `` ```mermaid `` にするだけで図形が描画されます。

### フローチャート

```mermaid
flowchart TD
    A([🚀 開始]) --> B{条件分岐}
    B -->|Yes| C[処理A]
    B -->|No| D[処理B]
    C --> E[(データベース)]
    D --> E
    E --> F([✅ 終了])

    style A fill:#4CAF50,color:#fff,stroke:#388E3C
    style F fill:#2196F3,color:#fff,stroke:#1565C0
    style B fill:#FF9800,color:#fff,stroke:#E65100
    style E fill:#9C27B0,color:#fff,stroke:#6A1B9A
```

**書き方：**

````md
```mermaid
flowchart TD
    A([🚀 開始]) --> B{条件分岐}
    B -->|Yes| C[処理A]
    B -->|No| D[処理B]
    C --> E[(データベース)]
    D --> E
    E --> F([✅ 終了])
```
````

---

### シーケンス図

```mermaid
sequenceDiagram
    autonumber
    participant U as 👤 ユーザー
    participant F as 🖥️ フロントエンド
    participant B as ⚙️ バックエンド
    participant D as 🗄️ データベース

    U->>F: リクエスト送信
    F->>B: API呼び出し
    B->>D: クエリ実行
    D-->>B: 結果返却
    B-->>F: JSONレスポンス
    F-->>U: 画面表示
```

**書き方：**

````md
```mermaid
sequenceDiagram
    participant U as ユーザー
    participant F as フロントエンド
    participant B as バックエンド
    participant D as データベース

    U->>F: リクエスト送信
    F->>B: API呼び出し
    B->>D: クエリ実行
    D-->>B: 結果返却
    B-->>F: JSONレスポンス
    F-->>U: 画面表示
```
````

---

### クラス図

```mermaid
classDiagram
    class Animal {
        +String name
        +int age
        +makeSound() void
        +move() void
    }
    class Dog {
        +String breed
        +fetch() void
        +makeSound() void
    }
    class Cat {
        +bool isIndoor
        +purr() void
        +makeSound() void
    }
    class Bird {
        +float wingspan
        +fly() void
        +makeSound() void
    }

    Animal <|-- Dog : 継承
    Animal <|-- Cat : 継承
    Animal <|-- Bird : 継承
```

**書き方：**

````md
```mermaid
classDiagram
    class Animal {
        +String name
        +makeSound() void
    }
    class Dog {
        +String breed
        +makeSound() void
    }
    Animal <|-- Dog : 継承
```
````

---

### ガントチャート

```mermaid
gantt
    title プロジェクト スケジュール
    dateFormat  YYYY-MM-DD
    section 設計フェーズ
    要件定義       :done,    req,  2024-01-01, 2024-01-14
    基本設計       :done,    des,  2024-01-15, 2024-01-28
    section 開発フェーズ
    バックエンド実装 :active,  back, 2024-01-29, 2024-02-25
    フロントエンド実装:         front,2024-02-01, 2024-02-25
    section テストフェーズ
    単体テスト      :         unit, 2024-02-26, 2024-03-10
    結合テスト      :         int,  2024-03-11, 2024-03-24
    section リリース
    本番リリース     :         rel,  2024-03-25, 2024-03-26
```

**書き方：**

````md
```mermaid
gantt
    title プロジェクト スケジュール
    dateFormat  YYYY-MM-DD
    section 設計フェーズ
    要件定義 :done, req, 2024-01-01, 2024-01-14
    基本設計 :done, des, 2024-01-15, 2024-01-28
    section 開発フェーズ
    実装     :active, dev, 2024-01-29, 2024-02-25
```
````

---

### 円グラフ

```mermaid
pie title 技術スタック比率
    "JavaScript" : 35
    "Python"     : 25
    "Go"         : 20
    "Rust"       : 12
    "その他"      : 8
```

**書き方：**

````md
```mermaid
pie title 技術スタック比率
    "JavaScript" : 35
    "Python"     : 25
    "Go"         : 20
    "その他"      : 20
```
````

---

### ER図

```mermaid
erDiagram
    USER {
        int id PK
        string name
        string email
        datetime created_at
    }
    ORDER {
        int id PK
        int user_id FK
        decimal total_price
        string status
        datetime ordered_at
    }
    PRODUCT {
        int id PK
        string name
        decimal price
        int stock
    }
    ORDER_ITEM {
        int id PK
        int order_id FK
        int product_id FK
        int quantity
    }

    USER ||--o{ ORDER : "注文する"
    ORDER ||--|{ ORDER_ITEM : "含む"
    PRODUCT ||--o{ ORDER_ITEM : "含まれる"
```

**書き方：**

````md
```mermaid
erDiagram
    USER {
        int id PK
        string name
        string email
    }
    ORDER {
        int id PK
        int user_id FK
        decimal total_price
    }
    USER ||--o{ ORDER : "注文する"
```
````

---

## 2. SVG 画像

SVGファイルをリポジトリに配置し、通常の画像と同じように参照できます。

```md
![図形サンプル](figures/shapes.svg)
```

![図形サンプル](figures/shapes.svg)

SVGは `<img>` タグでサイズを指定して表示することもできます：

```md
<img src="figures/shapes.svg" alt="基本図形" width="500">
```

<img src="figures/shapes.svg" alt="基本図形" width="500">

---

## 3. HTMLテーブルによるビジュアル表現

GitHubのMarkdownでは一部のHTML要素が使用できます。

### バッジ（Shields.io）

Shields.ioを使ってステータスバッジを表示できます：

```md
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Language](https://img.shields.io/badge/language-Markdown-lightgrey.svg)
![Mermaid](https://img.shields.io/badge/diagram-Mermaid-ff3670.svg)
```

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Language](https://img.shields.io/badge/language-Markdown-lightgrey.svg)
![Mermaid](https://img.shields.io/badge/diagram-Mermaid-ff3670.svg)

### HTMLテーブルとインラインSVG

```html
<table>
  <tr>
    <th>図形</th>
    <th>SVG</th>
    <th>説明</th>
  </tr>
  <tr>
    <td>四角形</td>
    <td><svg width="60" height="40"><rect width="60" height="40" fill="#3949ab" rx="4"/></svg></td>
    <td><code>&lt;rect&gt;</code> タグを使用</td>
  </tr>
  <tr>
    <td>円</td>
    <td><svg width="60" height="40"><circle cx="30" cy="20" r="18" fill="#00897b"/></svg></td>
    <td><code>&lt;circle&gt;</code> タグを使用</td>
  </tr>
  <tr>
    <td>三角形</td>
    <td><svg width="60" height="40"><polygon points="30,2 58,38 2,38" fill="#f57c00"/></svg></td>
    <td><code>&lt;polygon&gt;</code> タグを使用</td>
  </tr>
</table>
```

<table>
  <tr>
    <th>図形</th>
    <th>SVG</th>
    <th>説明</th>
  </tr>
  <tr>
    <td>四角形</td>
    <td><svg width="60" height="40"><rect width="60" height="40" fill="#3949ab" rx="4"/></svg></td>
    <td><code>&lt;rect&gt;</code> タグを使用</td>
  </tr>
  <tr>
    <td>円</td>
    <td><svg width="60" height="40"><circle cx="30" cy="20" r="18" fill="#00897b"/></svg></td>
    <td><code>&lt;circle&gt;</code> タグを使用</td>
  </tr>
  <tr>
    <td>三角形</td>
    <td><svg width="60" height="40"><polygon points="30,2 58,38 2,38" fill="#f57c00"/></svg></td>
    <td><code>&lt;polygon&gt;</code> タグを使用</td>
  </tr>
</table>

---

## 4. テキストアート（AAアート）

コードブロックを使ってテキストアートで図形を表現できます。

### 基本図形

```
┌─────────────────────────────────────────┐
│              四角形（長方形）              │
└─────────────────────────────────────────┘

     ●
    ●●●
   ●●●●●    ◀ 三角形（テキスト）
  ●●●●●●●
 ●●●●●●●●●

 ╔══════════╗
 ║  二重罫線  ║
 ╚══════════╝
```

### システム構成図

```
                    ┌──────────────────────────────────────┐
                    │            クラウド環境                │
                    │                                      │
  ┌──────────┐      │  ┌──────────┐      ┌──────────┐     │
  │          │      │  │          │      │          │     │
  │  ユーザー  │─────▶│  ロードバ  │─────▶│  アプリ   │     │
  │          │      │  │ ランサー   │      │ サーバー   │     │
  └──────────┘      │  └──────────┘      └─────┬────┘     │
                    │                          │           │
                    │                    ┌─────▼────┐     │
                    │                    │          │     │
                    │                    │   DB     │     │
                    │                    │ サーバー   │     │
                    │                    └──────────┘     │
                    └──────────────────────────────────────┘
```

### フローチャート（テキスト）

```
  開始
   │
   ▼
┌──────┐     はい    ┌──────────┐
│ 条件 │─────────▶ │  処理A   │
└──────┘           └────┬─────┘
   │ いいえ              │
   ▼                    │
┌──────────┐            │
│  処理B   │            │
└────┬─────┘            │
     └──────────────────┘
              │
              ▼
            終了
```

---

## 5. まとめ

| 方法 | GitHubサポート | 難易度 | 特徴 |
|------|--------------|--------|------|
| **Mermaid** | ✅ ネイティブ対応 | ⭐⭐ | テキストベースでバージョン管理しやすい |
| **SVG画像ファイル** | ✅ 完全サポート | ⭐⭐⭐ | 高品質・スケーラブル |
| **PNG/JPG画像** | ✅ 完全サポート | ⭐ | シンプルで汎用的 |
| **インラインSVG (HTML)** | ✅ 一部サポート | ⭐⭐⭐ | HTMLテーブル内で使用可 |
| **Shields.ioバッジ** | ✅ 完全サポート | ⭐ | ステータス表示に最適 |
| **テキストアート** | ✅ 完全サポート | ⭐⭐ | 軽量・依存関係なし |

> **💡 ヒント：** Mermaidはソースコードとともに図形をバージョン管理できるため、ドキュメントの保守性が高くなります。複雑な図形にはSVGファイルを使用することをお勧めします。

---

## 関連ファイル

- [`figures/shapes.svg`](figures/shapes.svg) - 基本図形のSVGサンプル
- [`generateAI/llm-local-overview.html`](generateAI/llm-local-overview.html) - ローカルLLMのインフォグラフィック（HTML版）
