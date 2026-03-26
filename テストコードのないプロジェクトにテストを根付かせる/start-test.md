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
 🗣️**Community**: AWS Community Builders
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

| パターン | 内容 |
|---|---|
| 一部だけ | 一部の機能にだけテストがある |
| 実行エラー | テストを実行するとエラーになる |
| UTのみ | Unit Testはあるが Integration Testはない |
| CI未整備 | テストはあるがCIで自動実行されていない |

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

# 古典学派テストの具体例

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
