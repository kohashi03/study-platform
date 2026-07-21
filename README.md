# Study Platform

複数科目に対応した、試験前の問題演習用Webアプリです。

## 主な機能

- 科目をJSONファイルとして追加
- 穴埋め・○×・四択・ランダム総合
- 「まだ解いていない問題」だけを出題
- 全問・誤答問題・「わからない」問題・直近正解問題の絞り込み
- 問題ごとの学習記録
- 苦手問題・復習資料の分析
- 学習記録の書き出し・読み込み
- 学習記録は利用者ごとのブラウザ内に保存
- 連続学習日数など、試験対策に不要な機能は非搭載

## GitHub Desktopでの初回設置

1. GitHub Desktopで `study-platform` を選択します。
2. `Show in Finder` を押します。
3. このZIP内のファイルとフォルダを、開いた `study-platform` フォルダへコピーします。
4. GitHub Desktopへ戻ります。
5. Summaryに `Study Platform initial release` と入力します。
6. `Commit to main` を押します。
7. 上部の `Push origin` を押します。

## GitHub Pagesの公開

1. GitHub Desktopの `View on GitHub` を押します。
2. リポジトリ上部の `Settings` を開きます。
3. 左側の `Pages` を開きます。
4. `Build and deployment` の Sourceを `Deploy from a branch` にします。
5. Branchを `main`、フォルダを `/(root)` にして保存します。
6. 数分後、表示されたURLを開きます。

通常のURLは次の形式です。

`https://ユーザー名.github.io/study-platform/`

## 科目の追加方法

1. `data` フォルダに、新しい科目のJSONを追加します。
2. `data/subjects.json` の `subjects` 配列に科目情報を追加します。
3. GitHub DesktopでCommitし、Pushします。

## 問題データの基本形

```json
{
  "id": "unique-question-id",
  "type": "fill",
  "q": "問題文",
  "answer": "正解",
  "aliases": ["別解"],
  "explanation": "解説",
  "source": {
    "displayFile": "授業資料.pdf",
    "pages": "15〜17",
    "pageTarget": 15,
    "topic": "テーマ",
    "url": null
  }
}
```

`type` は次のいずれかです。

- `fill`：穴埋め
- `tf`：○×。`answer` は `true` または `false`
- `mcq`：四択。`options` を付け、`answer` は0から始まる正解番号

## 授業資料リンクについて

授業スライドをGitHub Pagesに公開すると、インターネット上から閲覧可能になります。
担当教員の許可や配布条件を確認してから公開してください。

許可されている資料だけを公開する場合は、資料を `materials` 以下へ置き、各問題の
`source.url` に相対URLを設定します。

例：

```json
"url": "materials/educational-organization/lesson-04.pdf"
```

資料を公開しない場合は `null` のままで問題ありません。アプリにはファイル名とページ番号だけが表示されます。
