---
marp: true
theme: default
paginate: true
color: #000000
style: |
  @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500&display=swap');
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
    font-family: 'Fira Code', monospace;
  }
  table {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 10px 25px rgba(0,0,0,0.05);
    border: 1px solid #94a3b8;
    background-color: #ffffff;
  }
  th {
    background-color: #cbd5e1;
    color: #475569;
    font-weight: 700;
    padding: 20px 32px;
    text-align: left;
    border-bottom: 2px solid #94a3b8 !important;
    border-right: 1px solid #94a3b8 !important;
    letter-spacing: 0.05em;
  }
  th:last-child {
    border-right: none !important;
  }
  td {
    padding: 20px 32px;
    border-bottom: 1px solid #94a3b8 !important;
    border-right: 1px solid #94a3b8 !important;
    vertical-align: middle;
    color: #475569;
  }
  td:last-child {
    border-right: none !important;
  }
  tr:last-child td {
    border-bottom: none !important;
  }
  tr:nth-child(even) td {
    background-color: #fafafa;
  }
  pre {
    background-color: #1e1e1e;
    border-radius: 12px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    border: 1px solid #333;
    padding: 32px;
    padding-top: 56px;
    position: relative;
    overflow: hidden;
  }
  pre::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 40px;
    background-color: #2d2d2d;
    border-bottom: 1px solid #111;
    border-radius: 12px 12px 0 0;
  }
  pre::after {
    content: '';
    position: absolute;
    top: 14px;
    left: 16px;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background-color: #ff5f56;
    box-shadow: 20px 0 0 #ffbd2e, 40px 0 0 #27c93f;
  }
  pre code {
    background-color: transparent;
    color: #d4d4d4;
    font-family: 'Fira Code', monospace;
    font-size: 18px;
    line-height: 1.6;
  }
  .hljs-keyword { color: #56b6c2; }
  .hljs-meta { color: #c678dd; }
  .hljs-title { color: #e5c07b; }
  .hljs-title.class_ { color: #e5c07b; }
  .hljs-title.function_ { color: #61afef; }
  .hljs-comment { color: #7f848e; font-style: italic; }
  .hljs-string { color: #98c379; }
  .hljs-number { color: #d19a66; }
  .hljs-built_in { color: #e5c07b; }
  .callout {
    border-radius: 8px;
    padding: 12px 18px 14px;
    margin: 14px 0;
    border-left: 5px solid;
  }
  .callout::before {
    display: block;
    font-weight: 700;
    font-size: 0.8em;
    margin-bottom: 8px;
    letter-spacing: 0.05em;
  }
  .callout-info {
    background-color: #dbeafe;
    border-color: #3b82f6;
    color: #1e3a5f;
  }
  .callout-info::before {
    content: 'ℹ';
    color: #2563eb;
  }
  .callout-warn {
    background-color: #fef3c7;
    border-color: #f59e0b;
    color: #78350f;
  }
  .callout-warn::before {
    content: '⚠';
    color: #d97706;
  }
  .callout-erro {
    background-color: #fee2e2;
    border-color: #ef4444;
    color: #7f1d1d;
  }
  .callout-erro::before {
    content: '✖';
    color: #dc2626;
  }
  .callout-important {
    background-color: #ede9fe;
    border-color: #8b5cf6;
    color: #3b0764;
  }
  .callout-important::before {
    content: '★';
    color: #7c3aed;
  }
---

<!-- _class: title -->

## テストコードのないプロジェクトにテストを根付かせる

2026/05/30
JJUG CCC 2026 Spring
髙橋　透

---
<style scoped>
section {
  justify-content: flex-start;
}
</style>

![bg left:30% contain](../images/me.jpg)

### 髙橋　透@tttol777
 🧑‍💻**Role**: Backend Engineer
 ❤️**Like**: Java, AWS
 🗣️**Community**: JAWS-UG, AWS CBs
 👶**Others**: 一児の父

### Works
 🌐**Web**: https://about-tttol.link/
 🌐**SpeakerDeck**: https://speakerdeck.com/tttol

---

# このセッションで話すこと

テストがないあるいは機能していないプロジェクトに参画したとき
あなたならどうしますか？

<br>

- テストを導入するための技術的なステップ
- チームの合意を得るための対話の進め方

を共有します。

```
※本セッションで言及するテストとはJUnitなどのテストフレームワークによって実装されるテストコードを指しています。
```

---

# アジェンダ

1. 現状分析
2. テストがない/少ない原因
3. テスト強化を提案する
4. テストを実装する
5. CIによる自動化
6. 小さな成功体験を作る
7. テストを書く習慣がつくまで見守る

---

<!-- _class: title -->

# 1. 現状分析

---

# まずコードベースを読む

git clone してテストコードの実装状況を確認するところから始める。

---

# テストがゼロの場合
- コードベースからわかることはあまりない
- マニュアルテストの試験書など他の試験をあたる

---

# テストがある場合の確認ポイント

テストコードはあるが、正しく機能しているかを確認する。

<div class="callout callout-info">
一部の機能にだけテストがある  <br/>
テストを実行するとエラーになる
it Testはあるが Integration Testはない
テストはあるがCIで自動実行されていない
</div>

---

<!-- _class: title -->

# 2. テストがない/少ない原因

---

# よくある理由

「テストを書く時間がない」
「テストを書く必要性がわからない」

<br/>

→ テストがあることの具体的なメリットを伝える必要がある

---

# テストがあることのメリット

| メリット | 説明 |
|---|---|
| デグレ検知 | 意図しない影響範囲の変更を早期発見 |
| リファクタの安心感 | テストがあればコードを大胆に改善できる |
| マニュアルテストが自動テストへ | 作業が増えるのではなく置き換わる |
| 開発リードタイム短縮 | 「速く開発するためにテストを書く」という感覚 |

<br/>

※ただし、テストが**適切に**実装されている場合に限る

---

<!-- _class: title -->

# 3. テスト強化をチームに提案する

---

# 提案の前に：既存コードベースへの敬意

「テストを書きましょう！」だけでは動かない。
提案の立ち回り方が最も重要。

<br>

まず大前提として**既存コードベースに敬意を払う**

---

もちろん敬意を払うだけではチームは動かない。具体的なメリットも同時に伝える。
※再掲↓

> | メリット | 説明 |
> |---|---|
> | デグレ検知 | 意図しない影響範囲の変更を早期発見 |
> | リファクタの安心感 | テストがあればコードを大胆に改善できる |
> | マニュアルテストが自動テストへ | 作業が増えるのではなく置き換わる |
> | 開発リードタイム短縮 | 「速く開発するためにテストを書く」という感覚 |

<br/> 

---


<!-- _class: title -->

# 4. テストを実装する

---

**① 最初から全機能のテストを書こうとしない**
- ハッピーパス（ド正常系）だけに絞る
- 「完璧なテスト」より「動くテストが1本ある」状態を目指す

**② テストの実装は自分もやる。むしろ自分がやる。**
- 「実装してください」と言うだけでは弱い
- 自ら実装して効果を確かめて見せる
---

# 既存テストがある場合

既存のテストが正しく動いているかを確認する。

<br>

チェックポイント：
1. テスト実行結果は OK / NG?
2. OKだとしてプロダクトコードを正しく検証できているか

<br>

あまりにひどいテストは思い切って削除するのも一つの選択肢

---


<!-- _class: title -->
# 古典学派スタイルでテストを書く

---

テスト対象のコントローラ：

```java
@RestController
@RequiredArgsConstructor
public class SomeController {

    private final HogeService hogeService;

    public ResponseEntity<Void> index() {
        // コントローラから3つのサービスメソッドを呼び出す
        hogeService.methodA();
        hogeService.methodB();
        hogeService.methodC();
        return ResponseEntity.ok().build();
    }
}
```

---
テストコード：
```java
@Test
void index_古典学派() throws Exception {
    // GIVEN: テスト用DBにデータを準備
    someRepository.insert(...);
    // WHEN / THEN
    mockMvc
        .perform(get("/"))
        .andExpect(status().isOk());

    // DBレコードチェック
    var expected = ...
    var actual = someRepository.findById(...);
    assertEquals(actual, expected);
}
```

---

つまり古典学派とは・・・
- モックを極力使わない
- 振る舞いに対してテストを書く

---

# ロンドン学派
対照的な派閥としてロンドン学派がある

```java
void index_ロンドン学派() {
    // GIVEN
    var mockService = mock(HogeService.class);
    // WHEN
    new SomeController(mockService).index();
    // THEN
    verify(mockService).methodA();
    verify(mockService).methodB();
    verify(mockService).methodC();
}
```


---
つまりロンドン学派とは・・・
- 依存クラスにはモックを使う
- 一つの関数に対する純粋なUnit Test

---
# 余談：どこまでモックにするか

```
「管理外の依存だけモックにする。管理下の依存は本物を使う。」
```

管理下：
- 依存するクラス（HogeService）
- DBのRepositoryクラス・Mapperクラス

管理外：
- 外部API
- AWS等のクラウドサービス（S3、SSM等）
    - localstackを使っても良いが🤔
- Kafka等のメッセージングサービス

---

# 余談：カバレッジは100%を目指さない
90%前後で十分。
カバレッジは **「自分達が認識しているケースの範囲内での網羅率」** でしかない
認知してないケースを独力で認知することはできない

---

<!-- _class: title -->
# 5. CIによる自動化

---

# 自動実行されないテストはいつか必ず腐る!

# テストコードとCIはセットで考える!

---

<style scoped>
section {
  justify-content: flex-start;
}
</style>

![bg right:30% contain](../images/awake.pmg)

# CIによるテストの自動実行は必須

- GitHub Actions
- GitLab CI
- AWS CodeBuild
- Jenkins

利用するツールはなんでもいい
とにかく自動化だ！


---

失敗を無視できない環境を作ることが重要

- CIが通っていないPRをマージさせない設定も可能
- Slack通知でテスト失敗を即時共有

---

<!-- _class: title -->

# 6. 小さな成功体験を作る

---

# 「テストがあってよかった！」体験を作る

大きなものでなくていい
テストを正しく実装していればそのうち訪れる

具体例：
- 機能改修時にデグレに気づくことができた
- マニュアルテストの対応コストが減った

---

成功体験をメンバーが実感することで：
- テスト実装へのモチベーションが高まる
- テストを書くことが文化になっていく

この体験が「根付かせる」ための最大の推進力になる。

---

<!-- _class: title -->
# 7. テストを書く習慣が
# つくまで見守る

---

習慣が浸透するまで見守る＝テストをサボるメンバーを指摘するということ。

「時間がないのでテストは後で書きます」<- 書かない

---

忙しさはテストをサボる理由にはならない
無条件に許容するとまたテストのないプロジェクトに戻る

やむを得ない場合は許容するが条件をつける：
- テスト実装のタスクをチケットなどで必ず管理する
- テスト実装の必要性が低い場合はそのことをソースコメントやPRなどに明記しておく


---

<!-- _class: title -->

# まとめ

---

# テストコードが根付くまでのステップ（再掲）

| ステップ | ポイント |
|---|---|
| ① 現状分析 | 判断より先に観察 |
| ② 原因の解明 | 「意図的か」「やむを得ないか」を切り分ける |
| ③ 提案 | 敬意を払い、メリットを伝える |
| ④ 実装 | 古典学派スタイルで始める |
| ⑤ CI自動化 | テストは自動実行されてこそ輝く |
| ⑥ 成功体験 | 小さな体験が文化を作る |
| ⑦ 見守る | 習慣が浸透するまで伴走する |

---

# 一番大事なこと

<br>

技術的なステップより先に：

<br>

既存コードベースとチームへの敬意

<br>

これがなければ、どれだけ正しい提案をしても
チームは動かない。

---

<!-- _class: title -->
# ご清聴ありがとうございました
