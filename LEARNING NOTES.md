---
marp: false
theme: default
paginate: true
---

# LEARNING NOTES

## About -概要

- 各章の学習メモ
- 理解のポイント
- 実践的な気づき
- 疑問点
- 実装した具体的なワークフロー
- 学んだベストプラクティス

## Index -目次

<!-- TOC -->

- [LEARNING NOTES](#learning-notes)
  - [About -概要](#about--概要)
  - [Index -目次](#index--目次)
  - [Contents -内容](#contents--内容)
    - [1.1 ソフトウェア開発](#11-ソフトウェア開発)
      - [1.1.1 複雑性と変化](#111-複雑性と変化)
      - [1.1.2 品質と期待値](#112-品質と期待値)
      - [1.1.3 不可避な試行錯誤](#113-不可避な試行錯誤)
    - [1.2 CI/CD](#12-cicd)
      - [1.2.1 継続的インテグレーション](#121-継続的インテグレーション)
      - [1.2.2 継続的デリバリー](#122-継続的デリバリー)
      - [あ](#あ)

<!-- /TOC -->

## Contents -内容

### 1.1 ソフトウェア開発

- **ソフトウェアエンジニアの仕事である「価値を届ける」為に必須なことは**
- **１）コードをソフトウェアへ変換し、正しく動作するか検証する**
- **２）ソフトウェアをユーザーが使える状態にする**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[価値を届ける]
        direction LR
        A[コード]
        B[ソフトウェア]
        C[価値]

        A --> B
        B --> C
    end

```

#### 1.1.1 複雑性と変化

- **ソフトウェアは多数の要素がある**
- **それらが互いに影響を及ぼし、時には予期せぬ振る舞いをする**
- **そしてニーズの多様化により市場環境や要件も日々変化する**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[ソフトウェアは複雑]
        A[多数の要素] --> C{ソフトウェア}
        B[要素間の相互作用] --> C
        C --> D[予期せぬ振る舞い]
        E[ニーズの多様化] --> F[市場環境の変化]
        E --> G[要件の変化]
    end

```

#### 1.1.2 品質と期待値

- **ソフトウェアは正しく動くことはもちろん**
- **軽快、使いやすい、情報漏えいにも気をつける**
- **ユーザーの期待値は上がり続け応えられなければあっさり見捨てられる**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[ ]
        F[ユーザーの<br>継続利用] --o E
        G[離脱リスク] --x E
        
        classDef lv2-box stroke:#5f5f5f,fill:#555555,color:#ffffff,stroke-width:3px;
        Outer2:::lv2-box
        subgraph Outer2[ユーザーの期待値]

                E[期待値の上昇]
                
                A[正しい動作]
                B[軽快な操作]
                C[使いやすさ]
                D[情報保護]
                
                E --> A
                E --> B
                E --> C
                E --> D
            end
    end
```

#### 1.1.3 不可避な試行錯誤

- **複雑で変化が早く品質も求められる**
- **事前計画は不可能、試行錯誤を繰り返し一歩一歩近づくしかない**
- **何度も繰り返す為には、ソフトウェア開発は継続的（Continuous）にならざるを得ない**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[ ]
        direction LR
        A[計画] --> B[実装]
        B --> C[検証]
        C --> D[改善]
        D --> A
            classDef lv2-box stroke:#5f5f5f,fill:#555555,color:#ffffff,stroke-width:3px;
            Outer2:::lv2-box
            subgraph Outer2[継続的な改善プロセス]
                direction LR
                E[複雑性への対応]
                F[変化への適応]
                G[品質の向上]
        end
    
        D --> Outer2
    end
    
```

### 1.2 CI/CD

- **ソフトウェア開発のライフサイクルを繰り返しながらユーザーへ価値を届ける**
- **自動化によって、変更のための試行錯誤のスピードが上がり、より迅速に価値を生み出せる**
- **CI/CDはスピード面でのメリットだけでなく、プロセスの継続性や品質管理にも貢献する**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[開発のライフサイクル]
        direction LR
        A[計画]
        B[開発]
        
            classDef lv2-box stroke:#5f5f5f,fill:#555555,color:#ffffff,stroke-width:3px;
            Outer2:::lv2-box
            subgraph Outer2[CI/CDの範囲]
                direction LR
                K[ビルド]
                L[テスト]
                M[リリース]

                K --> L
                L --> M
            end
        
        C[運用]

        A --> B
        B --> K
        M --> C
    end
```

#### 1.2.1 継続的インテグレーション

- **CIは継続的インテグレーション（Continuous Integration）の略称**
- **インテグレーションとは変更したコードをコードベースへ取り込み、検証する営み**
- **単にコードベースへ統合するだけではなく、「検証」する点が重要**
  
```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[継続的インテグレーション]
            classDef lv2-box stroke:#5f5f5f,fill:#555555,color:#ffffff,stroke-width:3px;
            Outer2:::lv2-box
            subgraph Outer2[ ]
                direction LR
                A["コードの統合頻度を上げる"]
                B["コンフリクトが減る"]
                C["繰り返し検証"]
                D["バグをすばやく発見・修正"]
                E["ソフトウェアが安定して動く"]

                A --> B
                A --> C
                B --> E
                C --> D
                D --> E
            end
        F["ユーザーの満足度が高まる"]
        G["チームへ自信を与える"]
    end

    E --> F
    E --> G
```

#### 1.2.2 継続的デリバリー

- **コードをどうにかしてユーザーへ送り届ける、この活動をリリース（Release）と呼ぶ**
- **リリースはヒューマンエラーが発生しやすい**
- **ソフトウェアによって異なる作業、手順も複雑化しやすいのに何度も実行する**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[ ]
            classDef lv2-box stroke:#5f5f5f,fill:#555555,color:#ffffff,stroke-width:3px;
            Outer2:::lv2-box
            subgraph Outer2[ ]
                direction LR
                  A[コード変更] -->|リリース| B[ユーザーへの配信]
            end
            Outer3:::lv2-box
            subgraph Outer3[課題]
                D[ヒューマンエラーのリスク]
                E[作業の複雑化]
            end

            Outer2 -.-> Outer3

    end
```

- **いつでも安全にリリースできる状態を保ち、ソフトウェアを繰り返し改善する（＝CD）**
- **CDは継続的デリバリー（Continuous Delivery）の略称**
- **「自動化」により人間が介在する余地を小さくすれば、繰り返しに強く、いつでも安全にユーザーへソフトウェアを届けられる**

```mermaid
flowchart TD
    classDef lv1-box stroke:#4f4f4f,fill:#444444,color:#ffffff,stroke-width:5px;
    Outer1:::lv1-box
    subgraph Outer1[ ]
        direction LR

            classDef lv2-box stroke:#5f5f5f,fill:#555555,color:#ffffff,stroke-width:3px;
            Outer2:::lv2-box
            subgraph Outer2[継続的デリバリー（CD）]
                direction LR
                M[リリース]
                N[品質を担保]
        
                Outer3 -->|自動化| M
                Outer3 -.-> N

                classDef lv3-box stroke:#6f6f6f,fill:#666666,color:#ffffff,stroke-width:3px;
                Outer3:::lv3-box
                subgraph Outer3[継続的インテグレーション（CI）]
                    direction TB
                    K[コード統合]
                    L[検証]
            
                    K --> L
                end
            end
        
        A[新機能追加]
        B[バグ]
        C[迅速な提供]
        D[繰り返しに強い]

        A --> Outer3
        B --> Outer3
        Outer2 -.-> C
        C === D
    end

```

#### あ
