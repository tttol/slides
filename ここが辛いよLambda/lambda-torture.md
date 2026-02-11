---
marp: true
theme: default
paginate: true
color: #000000
style: |
  section {
    font-family: 'Noto Sans JP', sans-serif;
    background: linear-gradient(to bottom, #7a9df5, #ffffff);
  }
  section.title {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-image: linear-gradient(rgba(255,255,255,0.80), rgba(255,255,255,0.60)), url('../images/redrock.jpeg');
    background-size: cover;
    background-position: center;
  }
  section.title h1 {
    font-size: 2.5em;
    color: #000;
  }
  strong {
    color: #000;
  }
  code {
    background-color: #e8f0fe;
    color: #1a73e8;
  }
  table {
    margin: 0 auto;
  }
  th {
    background-color: #d4eeff;
  }
---

<!-- _class: title -->

# ここが辛いよLambda

2026/02/19
JAWS-UG神戸#10
髙橋　透

---

# 今日話すこと

1. **250MBクォータ** の壁
2. **SAM or CDK** の選択

業務でLambdaをしっかり使う機会があり、
色々と辛かったことを共有します

---

# 250MBクォータとは

- Lambda関数には**容量の上限**がある
- 関数本体 + Lambda Layer = **合計250MBまで**
- 超過すると...

```
Unzipped size must be smaller than 262144000 bytes
```

---

# 250MBって足りるの？

- 小〜中規模の実装なら十分足りる
- しかし**依存ライブラリ**を含めると話が変わる

> 例: Oracle DB向けのコネクションライブラリを入れたら
> **約300MB**まで膨れ上がった

「Lambda 250MB」で検索すると困っている人が大勢...

---

# 250MBを超えたらどうする？

## 選択肢は2つ

| | 方法 | 向いているケース |
|---|---|---|
| ① | リソースを削って250MB未満にする | ちょっとだけ超過（〜255MB） |
| ② | **コンテナイメージ方式**に切り替える | 大幅に超過（300MB〜） |

---

# コンテナイメージ方式

- 2020年12月リリースの機能
- Dockerイメージとしてビルド → **ECRにPUSH**
- イメージサイズは**最大10GB**まで許容
  - zipスタイルの**40倍！**

---

# コンテナイメージ方式の落とし穴

途中からの切り替えは**大変**

- SAM/CDKの設定ファイルを**大幅に書き直し**
  - ソースコード差分が大きく出る
  - レビュアーへの説明コストが増加
- ECRに関する**IAMポリシー**が色々必要
  - 権限の弱いアカウントだと追加申請が必要に

---

# 250MBクォータ：どうすればよかったか

## 構築前に見積もること！

- 依存ライブラリの合計サイズを事前に確認
- **zipスタイル or コンテナイメージスタイル**を
  事前に確定させる

> 後から方式を変えるのは大変

---

# SAM or CDKの選択

Lambdaのデプロイ方法はいくつかある

| 方法 | 特徴 |
|---|---|
| **AWS SAM CLI** | サーバーレス向けに特化。手軽 |
| **AWS CDK / Terraform** | 王道のIaC。汎用的 |
| 手動リリース | 論外 |

---

# 今回SAMを選んだ理由

- Lambda関数1個のために CDK/Terraform は大掛かり
- SAMなら `sam build` → `sam deploy` でシンプル
- 設定ファイルも `template.yaml` と `samconfig.toml` だけ

初めて使ったが、中々便利だった

---

# SAMの辛かったところ

## 認知度の低さ

- チーム内で「聞いたことあるけどよく知らない」が多数
- 認知度が低いと...
  - PJ引き継ぎ時の**説明コスト増**
  - インフラチームへの依頼時にも**説明コスト増**
  - SAM CLIの細かなオプションが知られていない

---

# SAM：どうすればよかったか

## チーム内で採用済みのIaCに寄せる

- チーム内ではTerraformが使われている箇所があった
- **Terraformにしておけばよかった**と後悔
- 技術的に最適な選択 ≠ チームにとって最適な選択

---

# まとめ

1. **250MBクォータに気をつけろ**
   - 構築前に依存ライブラリの容量を見積もる
   - zip or コンテナイメージは事前に決める

2. **デプロイ手法はチームで考えて選定しよう**
   - 認知されていないツールは説明コストが上がる
   - チーム内の既存技術に寄せるのも大事

---

<!-- _class: title -->

# ありがとうございました
